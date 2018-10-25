## Good
```php   
public function addDirektVerkaeufe($db, $pArtNr)
{
    $vor12Monaten = time() - 365 * 24 * 60 * 60;

    $anzahl = $this->getCount($db, $vor12Monaten, $pArtNr);

    if ($anzahl != "") {
        $this->update($db, $anzahl, $pArtNr);
    }
}

private function getCount($db, $time, $sku)
{
    return $db->getOne("SELECT SUM(menge) FROM je_bestellung WHERE artnr = ? AND zeit > ? AND datum < DATE(NOW()) AND post_ident IS NULL AND geloescht = 0",
        array($sku, $time));
}

private function update($db, $count, $sku) {
    $db->query("UPDATE je_artikel_history SET verkauft = verkauft + $count WHERE artnr = ?", array($sku));
}
```