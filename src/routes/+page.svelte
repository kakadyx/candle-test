<script>
  import Calculator from '$lib/Calculator.svelte';

  const language = 'ru';
  const altLang = 'en';
  const siteUrl = 'https://candle-calculate.netlify.app';

  const t = {
    eyebrow: 'Candle Lab',
    heroTitle: 'Калькулятор воска и отдушки для свечей',
    heroLead: 'Бесплатный онлайн-калькулятор для расчёта воска и отдушки при изготовлении свечей. Добавляйте несколько калькуляторов, чтобы сравнивать разные объёмы баночек.',
    ratiosTitle: 'Коэффициенты',
    waxShareLabel: 'доля воска (от объема банки)',
    fragranceShareLabel: 'доля отдушки (от объема сухого воска)',
    formulaTitle: 'Формулы',
    formulaWax: 'Сухой воск = объем x 0.925',
    formulaFragrance: 'Отдушка = сухой воск x 0.05',
    languageLabel: 'Язык',
    faqTitle: 'Часто задаваемые вопросы',
    faq: [
      {
        q: 'Как рассчитать количество воска для свечи?',
        a: 'Чтобы рассчитать количество воска для свечи, нужно умножить объём банки (в миллилитрах) на плотность воска — 0,925. Например, для банки 200 мл потребуется 185 граммов сухого воска. Наш калькулятор свечей делает это автоматически.'
      },
      {
        q: 'Сколько отдушки добавлять в свечу?',
        a: 'Рекомендуемая дозировка ароматической отдушки — 5% от массы сухого воска. Для банки 200 мл это составит примерно 9,25 грамма отдушки. Калькулятор рассчитает точное количество для любого объёма.'
      },
      {
        q: 'Какой объём банки выбрать для свечи?',
        a: 'Самые популярные размеры банок для свечей: маленькая (120 мл), средняя (200 мл) и большая (300 мл). Выбор зависит от назначения — маленькие подходят для пробников и подарков, средние — универсальный вариант, большие — для длительного горения.'
      },
      {
        q: 'Как пользоваться калькулятором свечей?',
        a: 'Введите объём банки в миллилитрах и количество свечей в партии. Калькулятор мгновенно рассчитает необходимое количество воска и отдушки на одну свечу и на всю партию. Можно добавить несколько калькуляторов для сравнения разных размеров.'
      },
      {
        q: 'Подходит ли калькулятор для соевого воска?',
        a: 'Да, калькулятор использует стандартную плотность воска 0,925 г/мл, которая подходит для большинства типов воска: соевого, парафинового, кокосового и их смесей. Для точных расчётов можно учитывать незначительные отклонения в плотности конкретного воска.'
      },
    ],
    aboutTitle: 'О калькуляторе свечей',
    aboutText: 'Candle Lab — бесплатный онлайн-калькулятор для свечеваров. Рассчитайте точное количество воска и ароматической отдушки для изготовления свечей любого размера. Инструмент помогает начинающим и опытным мастерам экономить материалы и создавать свечи с идеальным ароматом. Поддерживает расчёт партий любого размера с пресетами популярных объёмов баночек.',
    footerText: 'Candle Lab — калькулятор для изготовления свечей',
  };

  const jsonLd = {
    "@context": "https://schema.org",
    "@graph": [
      {
        "@type": "WebApplication",
        "name": "Candle Lab — Калькулятор воска и отдушки для свечей",
        "description": "Бесплатный онлайн-калькулятор для расчёта воска и отдушки при изготовлении свечей. Рассчитайте точное количество материалов для любого объёма баночки.",
        "url": siteUrl,
        "applicationCategory": "UtilityApplication",
        "operatingSystem": "All",
        "offers": {
          "@type": "Offer",
          "price": "0",
          "priceCurrency": "RUB"
        },
        "inLanguage": ["ru", "en"],
        "browserRequirements": "Requires JavaScript"
      },
      {
        "@type": "FAQPage",
        "mainEntity": t.faq.map(item => ({
          "@type": "Question",
          "name": item.q,
          "acceptedAnswer": {
            "@type": "Answer",
            "text": item.a
          }
        }))
      },
      {
        "@type": "HowTo",
        "name": "Как рассчитать воск и отдушку для свечи",
        "description": "Пошаговая инструкция по расчёту количества воска и отдушки для изготовления свечей",
        "step": [
          {
            "@type": "HowToStep",
            "name": "Выберите объём банки",
            "text": "Выберите один из пресетов (120, 200 или 300 мл) или введите объём вручную в миллилитрах"
          },
          {
            "@type": "HowToStep",
            "name": "Укажите количество свечей",
            "text": "Введите количество свечей в партии для расчёта общего объёма материалов"
          },
          {
            "@type": "HowToStep",
            "name": "Получите результат",
            "text": "Калькулятор автоматически рассчитает количество сухого воска и отдушки на одну свечу и на всю партию"
          }
        ]
      }
    ]
  };
</script>

<svelte:head>
  <title>Калькулятор воска и отдушки для свечей — Candle Lab | Бесплатный онлайн расчёт</title>
  <meta name="description" content="Бесплатный онлайн-калькулятор для расчёта воска и отдушки при изготовлении свечей. Рассчитайте точное количество соевого воска, парафина и ароматизатора для любого объёма банки. Пресеты популярных размеров." />
  <meta name="keywords" content="калькулятор свечей, калькулятор воска, расчёт воска для свечей, калькулятор отдушки, изготовление свечей, свечной калькулятор, сколько воска на свечу, расчёт отдушки для свечей, калькулятор для свечеварения, candle calculator" />
  <link rel="canonical" href="{siteUrl}/" />
  <link rel="alternate" hreflang="ru" href="{siteUrl}/" />
  <link rel="alternate" hreflang="en" href="{siteUrl}/en/" />
  <link rel="alternate" hreflang="x-default" href="{siteUrl}/" />

  <!-- Open Graph -->
  <meta property="og:type" content="website" />
  <meta property="og:title" content="Калькулятор воска и отдушки для свечей — Candle Lab" />
  <meta property="og:description" content="Бесплатный онлайн-калькулятор для изготовления свечей. Рассчитайте воск и отдушку для любого объёма банки." />
  <meta property="og:url" content="{siteUrl}/" />
  <meta property="og:site_name" content="Candle Lab" />
  <meta property="og:locale" content="ru_RU" />
  <meta property="og:locale:alternate" content="en_US" />

  <!-- Twitter Card -->
  <meta name="twitter:card" content="summary" />
  <meta name="twitter:title" content="Калькулятор воска и отдушки для свечей — Candle Lab" />
  <meta name="twitter:description" content="Бесплатный онлайн-калькулятор для изготовления свечей. Рассчитайте воск и отдушку для любого объёма банки." />

  <!-- JSON-LD Structured Data -->
  {@html `<script type="application/ld+json">${JSON.stringify(jsonLd)}</script>`}
</svelte:head>

<main class="page">
  <header class="hero">
    <div class="hero-copy">
      <div class="brand">
        <span class="brand-icon" aria-hidden="true">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 64 64" fill="none">
            <rect x="18" y="22" width="28" height="34" rx="8" fill="#b77c5f" />
            <rect x="22" y="26" width="20" height="26" rx="6" fill="#d9ad96" />
            <rect x="30.5" y="18" width="3" height="6" rx="1.5" fill="#8b8367" />
            <path d="M32 6c6 6 6 14 0 18-6-4-6-12 0-18z" fill="#f2d5c1" />
            <path d="M32 10c3 4 3 8 0 11-3-3-3-7 0-11z" fill="#fff8f2" />
          </svg>
        </span>
        <p class="eyebrow">{t.eyebrow}</p>
      </div>
      <h1>{t.heroTitle}</h1>
      <p class="lead">{t.heroLead}</p>
    </div>
    <div class="hero-panel">
      <nav class="panel-actions" aria-label="Выбор языка">
        <div class="language-toggle" role="group" aria-label={t.languageLabel}>
          <span class="language-label">{t.languageLabel}</span>
          <div class="toggle-buttons">
            <a href="/" class="active" aria-current="page">RU</a>
            <a href="/en/">EN</a>
          </div>
        </div>
      </nav>
      <div class="panel-card info-card">
        <div class="info-stack">
          <div class="info-section">
            <p class="info-title">{t.ratiosTitle}</p>
            <div class="panel-metrics">
              <div>
                <p class="metric-value">92.5%</p>
                <p class="metric-label">{t.waxShareLabel}</p>
              </div>
              <div>
                <p class="metric-value">5%</p>
                <p class="metric-label">{t.fragranceShareLabel}</p>
              </div>
            </div>
          </div>
          <div class="info-section">
            <p class="info-title">{t.formulaTitle}</p>
            <p class="info-text">{t.formulaWax}</p>
            <p class="info-text">{t.formulaFragrance}</p>
          </div>
        </div>
      </div>
    </div>
  </header>

  <Calculator {language} />

  <section class="seo-content" aria-label="О калькуляторе">
    <h2>{t.aboutTitle}</h2>
    <p>{t.aboutText}</p>
  </section>

  <section class="faq" aria-label="Часто задаваемые вопросы" itemscope itemtype="https://schema.org/FAQPage">
    <h2>{t.faqTitle}</h2>
    {#each t.faq as item}
      <details class="faq-item" itemscope itemprop="mainEntity" itemtype="https://schema.org/Question">
        <summary itemprop="name">{item.q}</summary>
        <div class="faq-answer" itemscope itemprop="acceptedAnswer" itemtype="https://schema.org/Answer">
          <p itemprop="text">{item.a}</p>
        </div>
      </details>
    {/each}
  </section>

  <footer class="site-footer">
    <p>{t.footerText}</p>
  </footer>
</main>
