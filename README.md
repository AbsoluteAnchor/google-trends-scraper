[Google Trends Scraper](https://apify.com/viralanalyzer/google-trends-scraper?fpr=data)

# 📈 Google Trends Scraper — Interest Over Time, Related Queries & Daily Trends

> 🔗 [View on Apify Store](https://apify.com/viralanalyzer/google-trends-scraper) | 🇺🇸 English | 🇧🇷 Português

Scrape **Google Trends data** for any keyword: interest over time, related queries, related topics, and daily trending searches. Compare up to 5 keywords at once with geo-targeting, time ranges, and category filters. Pure HTTP — fast and lightweight, no browser needed.

## ✨ Features

- 📊 **Interest over time** — Timeline with search interest values (0-100) for each keyword
- 🔗 **Related queries** — Top and rising related search queries per keyword
- 🏷️ **Related topics** — Top and rising related topics with type classification
- 📅 **Daily trending searches** — Today's trending searches with traffic estimates and news articles
- 🌍 **Geo-targeting** — Filter by country/region (ISO 3166-1 alpha-2 codes)
- ⏰ **Flexible time ranges** — Past hour to all time (2004-present)
- 🗂️ **Category filtering** — Filter by Google Trends category (Finance, Food & Drink, etc.)
- 🌐 **9 languages** — English, Portuguese, Spanish, French, German, Italian, Japanese, Korean, Chinese
- ⚡ **Pure HTTP** — Uses Google Trends internal API directly, no browser needed

## 📥 Input

| Parameter | Type | Required | Default | Description |
| --- | --- | --- | --- | --- |
| `keywords` | string[] | ✅ | — | Search terms to analyze (1-5 keywords) |
| `geo` | string | ❌ | `""` (worldwide) | Country code (e.g., "US", "BR", "GB") |
| `timeRange` | string | ❌ | `"today 12-m"` | Time period (see options below) |
| `category` | integer | ❌ | `0` | Google Trends category ID (0 = All) |
| `dataTypes` | string[] | ❌ | `["interestOverTime", "relatedQueries", "relatedTopics"]` | Data types to collect |
| `includeDailyTrends` | boolean | ❌ | `false` | Also fetch today's trending searches |
| `language` | string | ❌ | `"en"` | Results language (en, pt, es, fr, de, it, ja, ko, zh-CN) |
| `proxyConfiguration` | object | ❌ | Apify Proxy | Proxy settings |

**Time Range Options:**

| Value | Description |
| --- | --- |
| `now 1-H` | Past hour |
| `now 4-H` | Past 4 hours |
| `now 1-d` | Past day |
| `now 7-d` | Past 7 days |
| `today 1-m` | Past 30 days |
| `today 3-m` | Past 90 days |
| `today 12-m` | Past 12 months |
| `today 5-y` | Past 5 years |
| `all` | 2004 to present |

### Input Example

```
{
  "keywords": [
    "artificial intelligence",
    "machine learning",
    "deep learning"
  ],
  "geo": "US",
  "timeRange": "today 12-m",
  "category": 0,
  "dataTypes": ["interestOverTime", "relatedQueries", "relatedTopics"],
  "includeDailyTrends": true,
  "language": "en"
}
```

## 📤 Output

The actor produces 4 types of output items, all with a unified schema:

### Interest Over Time

| Field | Type | Description |
| --- | --- | --- |
| `type` | string | Always `"interestOverTime"` |
| `keyword` | string | The search term |
| `geo` | string | Country/region or `"worldwide"` |
| `timeRange` | string | Time period used |
| `timelinePoints` | number | Number of data points |
| `averageInterest` | number | Average interest value (0-100) |
| `maxInterest` | number | Peak interest value |
| `minInterest` | number | Minimum interest value |
| `timeline` | object[] | Array of `{date, timestamp, value, formattedValue}` |

### Related Queries

| Field | Type | Description |
| --- | --- | --- |
| `type` | string | Always `"relatedQueries"` |
| `keyword` | string | The search term |
| `rankingType` | string | `"TOP"` or `"RISING"` |
| `queriesCount` | number | Number of related queries |
| `queries` | object[] | Array of `{query, value, formattedValue, link}` |

### Related Topics

| Field | Type | Description |
| --- | --- | --- |
| `type` | string | Always `"relatedTopics"` |
| `keyword` | string | The search term |
| `rankingType` | string | `"TOP"` or `"RISING"` |
| `topicsCount` | number | Number of related topics |
| `topics` | object[] | Array of `{title, topicType, value, formattedValue, link}` |

### Daily Trends

| Field | Type | Description |
| --- | --- | --- |
| `type` | string | Always `"dailyTrends"` |
| `date` | string | Date of trending searches |
| `searchesCount` | number | Number of trending searches |
| `searches` | object[] | Array of `{title, traffic, trafficNumber, articles[]}` |

### Output Example

```
{
  "type": "interestOverTime",
  "keyword": "artificial intelligence",
  "geo": "US",
  "timeRange": "today 12-m",
  "language": "en",
  "category": 0,
  "timelinePoints": 52,
  "averageInterest": 71,
  "maxInterest": 100,
  "minInterest": 48,
  "timeline": [
    {
      "date": "Mar 10 – 16, 2025",
      "timestamp": 1741564800,
      "value": 62,
      "formattedValue": "62"
    },
    {
      "date": "Mar 17 – 23, 2025",
      "timestamp": 1742169600,
      "value": 68,
      "formattedValue": "68"
    }
  ],
  "scrapedAt": "2026-03-06T14:30:12.789Z"
}
```

```
{
  "type": "relatedQueries",
  "keyword": "artificial intelligence",
  "geo": "US",
  "timeRange": "today 12-m",
  "rankingType": "TOP",
  "queriesCount": 25,
  "queries": [
    {
      "query": "chatgpt",
      "value": 100,
      "formattedValue": "100",
      "link": "/trends/explore?q=chatgpt&geo=US"
    },
    {
      "query": "ai artificial intelligence",
      "value": 82,
      "formattedValue": "82",
      "link": "/trends/explore?q=ai+artificial+intelligence&geo=US"
    }
  ],
  "scrapedAt": "2026-03-06T14:30:15.123Z"
}
```

```
{
  "type": "dailyTrends",
  "keyword": "",
  "geo": "US",
  "date": "2026-03-06",
  "searchesCount": 20,
  "searches": [
    {
      "title": "March Madness",
      "traffic": "2,000,000+",
      "trafficNumber": 2000000,
      "articlesCount": 8,
      "articles": [
        {
          "title": "NCAA Tournament bracket revealed: Full field of 68 teams",
          "url": "https://www.espn.com/mens-college-basketball/story/_/id/43851273",
          "source": "ESPN",
          "snippet": "The 2026 NCAA Tournament bracket has been revealed..."
        }
      ]
    }
  ],
  "scrapedAt": "2026-03-06T14:30:18.456Z"
}
```

## 📋 Use Cases

- 📝 **Content Strategy** — Identify trending topics to create timely content
- 🔎 **SEO Research** — Discover rising search queries and related keywords
- 📊 **Market Research** — Compare product/brand interest over time and by region
- 🏢 **Competitive Analysis** — Track competitor brand search interest vs. yours
- 📈 **Trend Forecasting** — Analyze seasonal patterns and emerging trends
- 📰 **News Monitoring** — Track daily trending searches with related articles

## ❓ FAQ

**Q: How many keywords can I compare at once?**

A: Up to 5 keywords simultaneously, which is the limit imposed by Google Trends itself. Each keyword generates separate data items for interest over time, related queries (TOP + RISING), and related topics (TOP + RISING).

**Q: What do the interest values (0-100) mean?**

A: Google Trends normalizes search interest on a 0-100 scale relative to the peak popularity within the selected time range and region. A value of 100 represents peak popularity, 50 means half as popular as the peak, and 0 means insufficient data. These are relative values, not absolute search volumes.

**Q: Do I need a proxy?**

A: Google Trends may rate-limit requests, especially for multiple consecutive runs. For occasional use, no proxy is needed. For frequent or high-volume scraping, configure Apify Proxy via the `proxyConfiguration` parameter to avoid 429 errors.

**Q: What is the difference between TOP and RISING related queries?**

A: TOP queries are the most popular related searches overall for the keyword. RISING queries are those with the biggest increase in search frequency recently — these are especially useful for spotting emerging trends.

**Q: How does daily trends differ from keyword analysis?**

A: Keyword analysis (`interestOverTime`, `relatedQueries`, `relatedTopics`) shows data for your specific keywords. Daily trends (`includeDailyTrends`) returns what is trending today in the selected country regardless of your keywords — it includes traffic estimates and related news articles.

## 💰 Pricing

This actor uses **Pay Per Event (PPE)** pricing:

| Metric | Cost |
| --- | --- |
| Per data item scraped | $0.10 |

Each keyword generates multiple items (interest over time + related queries TOP + related queries RISING + related topics TOP + related topics RISING). Daily trends count as 1 item per day.

## 🔗 Related Actors

- [eBay Product Scraper](https://apify.com/viralanalyzer/ebay-product-scraper) — Product data for trend validation
- [CoinGecko Crypto Intelligence](https://apify.com/viralanalyzer/coingecko-crypto-intelligence) — Crypto market trends
- [Steam Game Intelligence](https://apify.com/viralanalyzer/steam-game-intelligence) — Gaming market trends
- [TikTok Viral Scanner](https://apify.com/viralanalyzer/tiktok-viral-scanner) — Viral content trends

## 📝 Changelog

### v1.0 (Current)

- Interest over time with full timeline data
- Related queries (TOP + RISING) per keyword
- Related topics (TOP + RISING) per keyword
- Daily trending searches with news articles (API + RSS fallback)
- Compare up to 5 keywords simultaneously
- Geo-targeting by country/region
- 9 time range options (past hour to all time)
- Category filtering
- 9 language options
- Anti-placeholder guardrails + contract validation
- Google XSSI prefix handling
- PPE billing integration

---

# 📈 Google Trends Scraper — Interesse ao Longo do Tempo, Consultas Relacionadas e Tendências

> 🔗 [View on Apify Store](https://apify.com/viralanalyzer/google-trends-scraper) | 🇺🇸 English | 🇧🇷 Português

Extraia **dados do Google Trends** para qualquer palavra-chave: interesse ao longo do tempo, consultas relacionadas, tópicos relacionados e buscas em alta do dia. Compare até 5 palavras-chave simultaneamente com filtros por país, período e categoria. HTTP puro — rápido e leve, sem browser.

## ✨ Funcionalidades

- 📊 **Interesse ao longo do tempo** — Timeline com valores de interesse de busca (0-100) por keyword
- 🔗 **Consultas relacionadas** — Principais e em crescimento por palavra-chave
- 🏷️ **Tópicos relacionados** — Principais e em crescimento com classificação de tipo
- 📅 **Buscas em alta do dia** — Tendências do dia com estimativas de tráfego e artigos de notícias
- 🌍 **Segmentação geográfica** — Filtre por país/região (códigos ISO 3166-1 alpha-2)
- ⏰ **Períodos flexíveis** — Última hora até todo o período (2004-presente)
- 🗂️ **Filtro por categoria** — Filtre por categoria do Google Trends (Finanças, Gastronomia, etc.)
- 🌐 **9 idiomas** — Inglês, Português, Espanhol, Francês, Alemão, Italiano, Japonês, Coreano, Chinês
- ⚡ **HTTP puro** — Usa API interna do Google Trends diretamente, sem browser

## 📥 Entrada

| Parâmetro | Tipo | Obrigatório | Padrão | Descrição |
| --- | --- | --- | --- | --- |
| `keywords` | string[] | ✅ | — | Termos de busca para analisar (1-5 keywords) |
| `geo` | string | ❌ | `""` (mundial) | Código do país (ex: "US", "BR", "GB") |
| `timeRange` | string | ❌ | `"today 12-m"` | Período de tempo (veja opções abaixo) |
| `category` | inteiro | ❌ | `0` | ID de categoria do Google Trends (0 = Todas) |
| `dataTypes` | string[] | ❌ | `["interestOverTime", "relatedQueries", "relatedTopics"]` | Tipos de dados para coletar |
| `includeDailyTrends` | boolean | ❌ | `false` | Incluir buscas em alta do dia |
| `language` | string | ❌ | `"en"` | Idioma dos resultados (en, pt, es, fr, de, it, ja, ko, zh-CN) |
| `proxyConfiguration` | objeto | ❌ | Apify Proxy | Configuração de proxy |

**Opções de Período:**

| Valor | Descrição |
| --- | --- |
| `now 1-H` | Última hora |
| `now 4-H` | Últimas 4 horas |
| `now 1-d` | Último dia |
| `now 7-d` | Últimos 7 dias |
| `today 1-m` | Últimos 30 dias |
| `today 3-m` | Últimos 90 dias |
| `today 12-m` | Últimos 12 meses |
| `today 5-y` | Últimos 5 anos |
| `all` | 2004 até o presente |

### Exemplo de Entrada

```
{
  "keywords": [
    "inteligência artificial",
    "machine learning",
    "deep learning"
  ],
  "geo": "BR",
  "timeRange": "today 12-m",
  "category": 0,
  "dataTypes": ["interestOverTime", "relatedQueries", "relatedTopics"],
  "includeDailyTrends": true,
  "language": "pt"
}
```

## 📤 Saída

O actor produz 4 tipos de itens de saída, todos com schema unificado:

### Interesse ao Longo do Tempo

| Campo | Tipo | Descrição |
| --- | --- | --- |
| `type` | string | Sempre `"interestOverTime"` |
| `keyword` | string | O termo de busca |
| `geo` | string | País/região ou `"worldwide"` |
| `timeRange` | string | Período utilizado |
| `timelinePoints` | número | Número de pontos de dados |
| `averageInterest` | número | Interesse médio (0-100) |
| `maxInterest` | número | Pico de interesse |
| `minInterest` | número | Mínimo de interesse |
| `timeline` | objeto[] | Array de `{date, timestamp, value, formattedValue}` |

### Consultas Relacionadas

| Campo | Tipo | Descrição |
| --- | --- | --- |
| `type` | string | Sempre `"relatedQueries"` |
| `keyword` | string | O termo de busca |
| `rankingType` | string | `"TOP"` ou `"RISING"` |
| `queriesCount` | número | Número de consultas relacionadas |
| `queries` | objeto[] | Array de `{query, value, formattedValue, link}` |

### Tópicos Relacionados

| Campo | Tipo | Descrição |
| --- | --- | --- |
| `type` | string | Sempre `"relatedTopics"` |
| `keyword` | string | O termo de busca |
| `rankingType` | string | `"TOP"` ou `"RISING"` |
| `topicsCount` | número | Número de tópicos relacionados |
| `topics` | objeto[] | Array de `{title, topicType, value, formattedValue, link}` |

### Tendências Diárias

| Campo | Tipo | Descrição |
| --- | --- | --- |
| `type` | string | Sempre `"dailyTrends"` |
| `date` | string | Data das buscas em alta |
| `searchesCount` | número | Número de buscas em alta |
| `searches` | objeto[] | Array de `{title, traffic, trafficNumber, articles[]}` |

### Exemplo de Saída

```
{
  "type": "interestOverTime",
  "keyword": "inteligência artificial",
  "geo": "BR",
  "timeRange": "today 12-m",
  "language": "pt",
  "category": 0,
  "timelinePoints": 52,
  "averageInterest": 65,
  "maxInterest": 100,
  "minInterest": 42,
  "timeline": [
    {
      "date": "10 – 16 de mar. de 2025",
      "timestamp": 1741564800,
      "value": 58,
      "formattedValue": "58"
    },
    {
      "date": "17 – 23 de mar. de 2025",
      "timestamp": 1742169600,
      "value": 63,
      "formattedValue": "63"
    }
  ],
  "scrapedAt": "2026-03-06T14:30:12.789Z"
}
```

## 📋 Casos de Uso

- 📝 **Estratégia de Conteúdo** — Identifique tópicos em alta para criar conteúdo oportuno
- 🔎 **Pesquisa de SEO** — Descubra consultas de busca em crescimento e palavras-chave relacionadas
- 📊 **Pesquisa de Mercado** — Compare interesse em produtos/marcas ao longo do tempo e por região
- 🏢 **Análise Competitiva** — Acompanhe o interesse de busca da marca concorrente vs. a sua
- 📈 **Previsão de Tendências** — Analise padrões sazonais e tendências emergentes
- 📰 **Monitoramento de Notícias** — Acompanhe buscas em alta do dia com artigos relacionados

## ❓ Perguntas Frequentes

**P: Quantas palavras-chave posso comparar ao mesmo tempo?**

R: Até 5 palavras-chave simultaneamente, que é o limite imposto pelo próprio Google Trends. Cada keyword gera itens separados para interesse ao longo do tempo, consultas relacionadas (TOP + RISING) e tópicos relacionados (TOP + RISING).

**P: O que significam os valores de interesse (0-100)?**

R: O Google Trends normaliza o interesse de busca em uma escala de 0-100 relativa ao pico de popularidade dentro do período e região selecionados. Um valor de 100 representa o pico de popularidade, 50 significa metade da popularidade do pico, e 0 significa dados insuficientes. São valores relativos, não volumes absolutos de busca.

**P: Preciso de proxy?**

R: O Google Trends pode aplicar rate limit em requisições, especialmente para múltiplas execuções consecutivas. Para uso ocasional, não é necessário proxy. Para scraping frequente ou em grande volume, configure o Apify Proxy através do parâmetro `proxyConfiguration` para evitar erros 429.

**P: Qual a diferença entre consultas TOP e RISING?**

R: Consultas TOP são as buscas relacionadas mais populares no geral para a keyword. Consultas RISING são aquelas com o maior aumento na frequência de busca recentemente — são especialmente úteis para identificar tendências emergentes.

**P: Como as tendências diárias diferem da análise de keywords?**

R: A análise de keywords (`interestOverTime`, `relatedQueries`, `relatedTopics`) mostra dados para suas palavras-chave específicas. Tendências diárias (`includeDailyTrends`) retorna o que está em alta hoje no país selecionado, independente das suas keywords — inclui estimativas de tráfego e artigos de notícias relacionados.

## 💰 Preços

Este actor usa precificação **Pay Per Event (PPE)**:

| Métrica | Custo |
| --- | --- |
| Por item de dados extraído | $0.10 |

Cada keyword gera múltiplos itens (interesse ao longo do tempo + consultas relacionadas TOP + consultas relacionadas RISING + tópicos relacionados TOP + tópicos relacionados RISING). Tendências diárias contam como 1 item por dia.

## 🔗 Actors Relacionados

- [eBay Product Scraper](https://apify.com/viralanalyzer/ebay-product-scraper) — Dados de produtos para validar tendências
- [CoinGecko Crypto Intelligence](https://apify.com/viralanalyzer/coingecko-crypto-intelligence) — Tendências de mercado cripto
- [Steam Game Intelligence](https://apify.com/viralanalyzer/steam-game-intelligence) — Tendências de mercado de jogos
- [TikTok Viral Scanner](https://apify.com/viralanalyzer/tiktok-viral-scanner) — Tendências de conteúdo viral

## 📝 Changelog

### v1.0 (Atual)

- Interesse ao longo do tempo com timeline completa
- Consultas relacionadas (TOP + RISING) por keyword
- Tópicos relacionados (TOP + RISING) por keyword
- Buscas em alta do dia com artigos de notícias (API + fallback RSS)
- Comparação de até 5 keywords simultaneamente
- Segmentação geográfica por país/região
- 9 opções de período (última hora até todos os tempos)
- Filtro por categoria
- 9 opções de idioma
- Guardrails anti-placeholder + validação de contrato
- Tratamento de prefixo XSSI do Google
- Integração com cobrança PPE