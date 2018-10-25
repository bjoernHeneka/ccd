## Bad
```php
public function addDirektVerkaeufe($pArtNr)
{
    global $db;

    $vor12Monaten = time() - 365 * 24 * 60 * 60;

    $anzahl = $db->getOne("SELECT SUM(menge) FROM je_bestellung WHERE artnr = ? AND zeit > ? AND datum < DATE(NOW()) AND post_ident IS NULL AND geloescht = 0",
        array($pArtNr, $vor12Monaten));

    if ($anzahl != "") {
        $db->query("UPDATE je_artikel_history SET verkauft = verkauft + $anzahl WHERE artnr = ?", array($pArtNr));
    }
}
```