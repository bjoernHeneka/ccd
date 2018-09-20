## Before
```php
const DATE_FORMAT = 'Y-m-d H:i:s';

    /**
     * @param Request $request
     * @param string $slug
     * @return string
     * @throws \Exception
     */
    public function showAction(Request $request, $slug)
    {
        $slug = $this->extractSlug($slug);
        $this->result = $this->getSearchResults($slug, $request);

        $this->initPageContext($slug);
        $this->createKairionData($slug);

        if (!empty($this->result['products']) && !$this->getUser()->isCrawler()) {
            $this->getDoctrineConnection()->insert('je_suche_top',
                ['keyword' => $slug, 'timestamp' => date(self::DATE_FORMAT)]);
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
            'epoqTrack' => $this->getEpoqTrackData(),
            'seoText' => $this->getSeoText($slug),
            'searchPhrase' => $slug,
            'content' => $this->getContent($request, $slug)
        ]);
    }

    private function extractSlug($slug) {
        if (false !== strpos($slug, '+')) {
            $slug = str_replace('+', ' ', $slug);
        }

        return $slug;
    }

    /**
     * @return array
     */
    private function getEpoqTrackData()
    {
        $epoqTrackData = array(
            'sid' => session_id()
        );
        if (isset($this->result['qid'])) {
            $epoqTrackData['qid'] = $this->result['qid'];
        }
        if ($this->getCustomer()) {
            $epoqTrackData['custId'] = $this->getCustomer()->getId();
        }
        return $epoqTrackData;
    }
```