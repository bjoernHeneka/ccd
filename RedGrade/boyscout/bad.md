## Before
```php
public function showAction(Request $request, $slug)
{
    if (false !== strpos($slug, '+')) {
        $slug = str_replace('+', ' ', $slug);
    }

    $this->result = $this->getSearchResults($slug, $request);

    $this->initPageContext($slug);
    $this->createKairionData($slug);

    $epoqTrackData = array(
        'sid' => session_id()
    );
    if (isset($this->result['qid'])) {
        $epoqTrackData['qid'] = $this->result['qid'];
    }
    if ($this->getCustomer()) {
        $epoqTrackData['custId'] = $this->getCustomer()->getId();
    }

    if (!empty($this->result['products']) && !$this->getUser()->isCrawler()) {
        $this->getDoctrineConnection()->insert('je_suche_top',
            ['keyword' => $slug, 'timestamp' => date('Y-m-d H:i:s')]);
    }

    $PageViewLogicProvider = PageViewLogicProvider::getInstance($this->app);
    $tpl = $this->app['twig']->loadTemplate('/catalog/search/defaultServer.twig');
    return $tpl->render([
        'GLOBAL' => $PageViewLogicProvider->getGlobalTwigVars(),
        'LOCALE' => self::LOCALE,
        'SearchParams' => $this->getParams(),
        'Sorting' => $this->getSorting(),
        'Paging' => $this->getPaging(),
        'Result' => $this->result,
        'epoqTrack' => $epoqTrackData,
        'seoText' => $this->getSeoText($slug),
        'searchPhrase' => $slug,
        'content' => $this->getContent($request, $slug)
    ]);
}
```