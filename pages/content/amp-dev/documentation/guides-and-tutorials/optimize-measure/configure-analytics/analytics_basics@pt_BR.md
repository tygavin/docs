---
$title: "Analytics: conceitos básicos"
---

Conheça os conceitos básicos da análise de AMP.

## Usar amp-pixel ou amp-analytics?

A AMP oferece dois componentes para atender às suas necessidades de análise e medição: [`amp-pixel`]({{g.doc('/content/amp-dev/documentation/components/reference/amp-pixel.md', locale=doc.locale).url.path}})
e [`amp-analytics`]({{g.doc('/content/amp-dev/documentation/components/reference/amp-analytics.md', locale=doc.locale).url.path}}). As duas opções enviam dados de análise para um ponto de extremidade definido.

Se você quiser um comportamento semelhante ao de um simples [pixel de rastreamento](https://en.wikipedia.org/wiki/Web_beacon#Implementation), o componente [`amp-pixel`]({{g.doc('/content/amp-dev/documentation/components/reference/amp-pixel.md', locale=doc.locale).url.path}}) fornecerá um rastreamento básico de exibições de página. Os dados de exibição de página são enviados para um URL definido. Algumas integrações com fornecedores podem precisar desse componente. Nesse caso, elas especificarão o ponto de extremidade exato do URL.

Na maioria das soluções de análise, use [`amp-analytics`]({{g.doc('/content/amp-dev/documentation/components/reference/amp-analytics.md', locale=doc.locale).url.path}}). O rastreamento de exibições de página também funciona em [`amp-analytics`]({{g.doc('/content/amp-dev/documentation/components/reference/amp-analytics.md', locale=doc.locale).url.path}}). No entanto, também é possível rastrear o engajamento dos usuários com qualquer tipo de conteúdo da página, incluindo cliques em links e botões. Além disso, você pode medir até onde o usuário rolou a página, se ele interagiu ou não com mídias sociais e muito mais.

Saiba mais: Consulte [Informações detalhadas sobre o AMP Analytics]({{g.doc('/content/amp-dev/documentation/guides-and-tutorials/optimize-measure/configure-analytics/deep_dive_analytics.md', locale=doc.locale).url.path}}).

Como parte da integração com a plataforma AMP, os fornecedores ofereceram configurações predefinidas de [`amp-analytics`]({{g.doc('/content/amp-dev/documentation/components/reference/amp-analytics.md', locale=doc.locale).url.path}})
para que seja mais fácil coletar dados e movê-los para suas ferramentas de rastreamento. Acesse a documentação de fornecedores na lista [Fornecedores de análise]({{g.doc('/content/amp-dev/documentation/guides-and-tutorials/optimize-measure/configure-analytics/analytics-vendors.md', locale=doc.locale).url.path}}).

Você pode usar [`amp-pixel`]({{g.doc('/content/amp-dev/documentation/components/reference/amp-pixel.md', locale=doc.locale).url.path}}) e [`amp-analytics`]({{g.doc('/content/amp-dev/documentation/components/reference/amp-analytics.md', locale=doc.locale).url.path}})
nas suas páginas: [`amp-pixel`]({{g.doc('/content/amp-dev/documentation/components/reference/amp-pixel.md', locale=doc.locale).url.path}}) para rastreamento simples de exibições de página e [`amp-analytics`]({{g.doc('/content/amp-dev/documentation/components/reference/amp-analytics.md', locale=doc.locale).url.path}}) para todo o restante. Também é possível adicionar várias instâncias de cada tag. Se estiver trabalhando com vários fornecedores de análise, será necessário usar uma tag por solução. As páginas AMP mais simples são melhores para os usuários, portanto se você não precisar de tags adicionais, não as use.

## Criar uma configuração de análise simples

Saiba como criar uma configuração simples de [`amp-pixel`]({{g.doc('/content/amp-dev/documentation/components/reference/amp-pixel.md', locale=doc.locale).url.path}}) e [`amp-analytics`]({{g.doc('/content/amp-dev/documentation/components/reference/amp-analytics.md', locale=doc.locale).url.path}}) .

### Configuração simples de amp-pixel

Para criar uma configuração simples de [`amp-pixel`]({{g.doc('/content/amp-dev/documentation/components/reference/amp-pixel.md', locale=doc.locale).url.path}}), insira algo parecido com o seguinte no corpo da página AMP:

```html
<amp-pixel src="https://foo.com/pixel?RANDOM"></amp-pixel>
```

Neste exemplo, os dados de exibição de página são enviados para o URL definido, juntamente com um número aleatório. A variável `RANDOM`
é uma entre as muitas [variáveis ​​de substituição na plataforma AMP](https://github.com/ampproject/amphtml/blob/master/spec/amp-var-substitutions.md). Saiba mais sobre a [substituição de variáveis]({{g.doc('/content/amp-dev/documentation/guides-and-tutorials/optimize-measure/configure-analytics/analytics_basics.md', locale=doc.locale).url.path}}#variable-substitution).

O componente [`amp-pixel`]({{g.doc('/content/amp-dev/documentation/components/reference/amp-pixel.md', locale=doc.locale).url.path}}) é integrado, de modo que não é necessário fazer uma declaração de inclusão, como ocorre com os componentes estendidos de AMP, incluindo [`amp-analytics`]({{g.doc('/content/amp-dev/documentation/components/reference/amp-analytics.md', locale=doc.locale).url.path}}). Entretanto, é necessário colocar a tag [`amp-pixel`]({{g.doc('/content/amp-dev/documentation/components/reference/amp-pixel.md', locale=doc.locale).url.path}}) o mais perto possível do início de `<body>`. O pixel de rastreamento será acionado somente quando a tag for exibida. Se [`amp-pixel`]({{g.doc('/content/amp-dev/documentation/components/reference/amp-pixel.md', locale=doc.locale).url.path}}) estiver posicionado perto da parte inferior da página, talvez ele não seja acionado.

### Configuração simples de `amp-analytics`

Para criar uma configuração simples de [`amp-analytics`]({{g.doc('/content/amp-dev/documentation/components/reference/amp-analytics.md', locale=doc.locale).url.path}}), primeiro é necessário incluir esta declaração `custom-element` no `<head>`
documento de AMP (consulte também [Declaração de inclusão de componente]({{g.doc('/content/amp-dev/documentation/components/index.html', locale=doc.locale).url.path}})):

```html
<script async custom-element="amp-analytics" src="https://cdn.ampproject.org/v0/amp-analytics-0.1.js"></script>
```

O exemplo a seguir é semelhante ao [exemplo de `amp-pixel`]({{g.doc('/content/amp-dev/documentation/components/reference/amp-pixel.md', locale=doc.locale).url.path}}). Todas as vezes que uma página estiver visível, o evento será acionado e enviará os dados de exibição de página para um URL definido, juntamente com um código aleatório:

```html
<amp-analytics>

<script type="application/json">

  {"requests":
    {"pageview": "https://foo.com/pixel?RANDOM
  ", },"triggers":
    {"trackPageview":
      {"on": "visible",
      "request": "pageview"

} } }</script>

</amp-analytics>
```

No exemplo acima, definimos uma solicitação chamada "pageview" como `https://foo.com/pixel?RANDOM`. Como visto anteriormente, RANDOM é substituído por um número aleatório, de modo que a solicitação será algo parecido com `https://foo.com/pixel?0.23479283687235653498734`.

Quando a página se tornar visível (como especificado pelo uso da palavra-chave de acionamento `visible`), um evento será acionado, e a solicitação `pageview` será enviada. O atributo "triggers" determinará quando a solicitação "pageview" será acionada. Saiba mais sobre [solicitações e acionamentos]({{g.doc('/content/amp-dev/documentation/guides-and-tutorials/optimize-measure/configure-analytics/deep_dive_analytics.md', locale=doc.locale).url.path}}#requests-triggers--transports).

## Substituição de variáveis

Tanto o componente [`amp-pixel`]({{g.doc('/content/amp-dev/documentation/components/reference/amp-pixel.md', locale=doc.locale).url.path}})
quanto [`amp-analytics`]({{g.doc('/content/amp-dev/documentation/components/reference/amp-analytics.md', locale=doc.locale).url.path}})
permitem todas as substituições de variáveis ​​de URL padrão (consulte [Substituições de variáveis ​​de AMP HTML](https://github.com/ampproject/amphtml/blob/master/spec/amp-var-substitutions.md)). No exemplo abaixo, a solicitação de exibição de página é enviada ao URL juntamente com o URL canônico do documento AMP atual, o title e um [código de cliente]({{g.doc('/content/amp-dev/documentation/guides-and-tutorials/optimize-measure/configure-analytics/analytics_basics.md', locale=doc.locale).url.path}}):

```html
<amp-pixel src="https://example.com/analytics?url=${canonicalUrl}&title=${title}&clientId=${clientId(site-user-id)}"></amp-pixel>
```

Por ser bastante simples, a tag [`amp-pixel`]({{g.doc('/content/amp-dev/documentation/components/reference/amp-pixel.md', locale=doc.locale).url.path}}) só pode incluir variáveis ​​definidas pela plataforma ou que possam ser analisadas pelo tempo de execução da AMP a partir da página AMP. No exemplo acima, a plataforma preenche os valores de `canonicalURL` e `clientId(site-user-id)`. A tag [`amp-analytics`]({{g.doc('/content/amp-dev/documentation/components/reference/amp-analytics.md', locale=doc.locale).url.path}}) pode incluir as mesmas variáveis que [`amp-pixel`]({{g.doc('/content/amp-dev/documentation/components/reference/amp-pixel.md', locale=doc.locale).url.path}}), assim como as variáveis ​​definidas de modo exclusivo dentro da configuração da tag.

Use o formato `${varName}` em strings de solicitação para variáveis definidas pela página ou pela plataforma. As variáveis [`amp-analytics`]({{g.doc('/content/amp-dev/documentation/components/reference/amp-analytics.md', locale=doc.locale).url.path}})
substituirão o modelo por seu valor real no momento da construção da solicitação de análise (consulte também [`amp-analytics`]({{g.doc('/content/amp-dev/documentation/components/reference/amp-analytics.md', locale=doc.locale).url.path}}).

No exemplo de [`amp-analytics`]({{g.doc('/content/amp-dev/documentation/components/reference/amp-analytics.md', locale=doc.locale).url.path}}) abaixo, a solicitação de exibição de página é enviada ao URL com dados adicionais extraídos de substituições de variáveis, algumas fornecidas pela plataforma, outras definidas in-line, dentro da configuração de [`amp-analytics`]({{g.doc('/content/amp-dev/documentation/components/reference/amp-analytics.md', locale=doc.locale).url.path}}):

```html
<amp-analytics>

<script type="application/json">

  {"requests":
    {"pageview":"https://example.com/analytics?url=${canonicalUrl}&title=${title}&acct=${account}&clientId=${clientId(site-user-id)}",
  },
  "vars":
    {"account":
  "ABC123", },"triggers":
    {"someEvent":
      {"on": "visible",
      "request": "pageview",
      "vars":
        {"title":
"Minha página inicial", } } } }</script>

</amp-analytics>
```

No exemplo acima, as variáveis `account` e `title` são definidas na configuração de [`amp-analytics`]({{g.doc('/content/amp-dev/documentation/components/reference/amp-analytics.md', locale=doc.locale).url.path}}). As variáveis `canonicalUrl` e `clientId` não são definidas na configuração, por isso os valores delas são substituídos pela plataforma.

Importante: a substituição de variáveis é flexível. As mesmas variáveis ​​podem ser definidas em locais diferentes, e o tempo de execução da AMP analisará os valores nessa ordem de precedência (consulte [Ordem da substituição de variáveis]({{g.doc('/content/amp-dev/documentation/guides-and-tutorials/optimize-measure/configure-analytics/deep_dive_analytics.md', locale=doc.locale).url.path}}#variable-substitution-ordering) ).

## Identificação do usuário

Os websites usam cookies para armazenar informações específicas dos usuários no navegador. Os cookies podem ser usados ​​para informar que um usuário já visitou um site antes. Na AMP, as páginas podem ser veiculadas pelo site de um editor ou por um cache (como o Google AMP Cache). O website do editor e o cache provavelmente terão domínios diferentes. Por motivos de segurança, os navegadores podem limitar o acesso a cookies de outros domínios (consulte também [Rastrear usuários em diferentes origens](https://github.com/ampproject/amphtml/blob/master/spec/amp-managing-user-state.md)).

Por padrão, a AMP fornecerá um código de cliente, seja a página acessada pelo site original do editor ou por um cache. O código de cliente gerado pela AMP tem o valor da string codificada `"amp-"` followed by a random `base64` e permanece o mesmo para o usuário, caso ele volte a acessar a página.

A AMP administra a leitura e a gravação do código de cliente em todos os casos. Isso é importante principalmente no caso de páginas veiculadas por meio de um cache ou de alguma outra forma fora do contexto de exibição do site original do editor. Nessa circunstância, o acesso aos cookies do site do editor não estará disponível.

Quando uma página AMP é veiculada pelo site do editor, é possível fazer com que a estrutura de código de cliente usada pela AMP busque e use um cookie substituto. Nesse caso, o argumento `cid-scope-cookie-fallback-name` da variável `clientId` será interpretado como o nome do cookie. A formatação pode aparecer como `CLIENT_ID(cid-scope-cookie-fallback-name)`
ou `${clientId(cid-scope-cookie-fallback-name)}`.

Por exemplo:

```html
<amp-pixel src="https://foo.com/pixel?cid=CLIENT_ID(site-user-id-cookie-fallback-name)"></amp-pixel>
```

Se a AMP descobrir que o cookie está definido, a substituição do código de cliente retornará o valor do cookie. Se a AMP descobrir que esse cookie não está definido, ela gerará um valor no formato `amp-` seguido de uma string aleatória codificada base64.

Saiba mais sobre a substituição do código de cliente, incluindo como adicionar um código de notificação de usuário opcional em [Variáveis ​​permitidas na análise de AMP](https://github.com/ampproject/amphtml/blob/master/extensions/[`amp-analytics`]({{g.doc('/content/amp-dev/documentation/components/reference/amp-analytics.md', locale=doc.locale).url.path}}) /analytics-vars.md).

Saiba mais: Continue seu aprendizado sobre análises em [Informações detalhadas sobre o AMP Analytics]({{g.doc('/content/amp-dev/documentation/guides-and-tutorials/optimize-measure/configure-analytics/deep_dive_analytics.md', locale=doc.locale).url.path}}) e [Casos de uso]({{g.doc('/content/amp-dev/documentation/guides-and-tutorials/optimize-measure/configure-analytics/use_cases.md', locale=doc.locale).url.path}}).
