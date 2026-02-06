<script>
  import Calculator from '$lib/Calculator.svelte';

  const language = 'en';
  const siteUrl = 'https://candle-calculate.netlify.app';

  const t = {
    eyebrow: 'Candle Lab',
    heroTitle: 'Candle Wax & Fragrance Calculator',
    heroLead: 'Free online candle making calculator. Calculate exactly how much wax and fragrance oil you need for any jar size. Add multiple calculators to compare different jar volumes side by side.',
    ratiosTitle: 'Ratios',
    waxShareLabel: 'wax share (of jar volume)',
    fragranceShareLabel: 'fragrance share (of dry wax)',
    formulaTitle: 'Formulas',
    formulaWax: 'Dry wax = volume x 0.925',
    formulaFragrance: 'Fragrance = dry wax x 0.05',
    languageLabel: 'Language',
    faqTitle: 'Frequently Asked Questions',
    faq: [
      {
        q: 'How do I calculate the amount of wax for a candle?',
        a: 'To calculate the wax needed for a candle, multiply the jar volume (in milliliters) by the wax density of 0.925. For example, a 200 ml jar requires 185 grams of dry wax. Our candle calculator does this automatically for any jar size.'
      },
      {
        q: 'How much fragrance oil should I add to a candle?',
        a: 'The recommended fragrance load is 5% of the dry wax weight. For a 200 ml jar, this equals approximately 9.25 grams of fragrance oil. The calculator computes the exact amount for any volume you enter.'
      },
      {
        q: 'What jar size should I choose for candle making?',
        a: 'The most popular candle jar sizes are: small (120 ml / 4 oz), medium (200 ml / 7 oz), and large (300 ml / 10 oz). Small jars work well for samples and gifts, medium jars are the universal choice, and large jars provide longer burn times.'
      },
      {
        q: 'How do I use this candle making calculator?',
        a: 'Enter the jar volume in milliliters and the number of candles in your batch. The calculator instantly shows the wax and fragrance needed per candle and for the entire batch. You can add multiple calculators to compare different jar sizes.'
      },
      {
        q: 'Does this calculator work for soy wax?',
        a: 'Yes, the calculator uses a standard wax density of 0.925 g/ml which works for most wax types including soy wax, paraffin wax, coconut wax, and blends. Minor density variations between specific wax brands have negligible impact on the results.'
      },
      {
        q: 'Can I calculate wax for a candle batch?',
        a: 'Yes. Enter the number of candles in the batch field and the calculator will multiply the per-candle wax and fragrance amounts by your batch size. This helps you plan material purchases and production runs efficiently.'
      },
    ],
    aboutTitle: 'About Candle Calculator',
    aboutText: 'Candle Lab is a free online candle making calculator designed for chandlers and crafters. Accurately calculate the amount of wax and fragrance oil needed for candles of any size. Whether you are a beginner or an experienced candle maker, this tool helps you save materials and create perfectly scented candles. Supports batch calculations with presets for popular jar sizes.',
    footerText: 'Candle Lab — Free Candle Making Calculator',
  };

  const jsonLd = {
    "@context": "https://schema.org",
    "@graph": [
      {
        "@type": "WebApplication",
        "name": "Candle Lab — Candle Wax & Fragrance Calculator",
        "description": "Free online candle making calculator. Calculate exactly how much wax and fragrance oil you need for any candle jar size.",
        "url": `${siteUrl}/en/`,
        "applicationCategory": "UtilityApplication",
        "operatingSystem": "All",
        "offers": {
          "@type": "Offer",
          "price": "0",
          "priceCurrency": "USD"
        },
        "inLanguage": ["en", "ru"],
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
        "name": "How to Calculate Wax and Fragrance for Candles",
        "description": "Step-by-step guide to calculating wax and fragrance oil amounts for candle making",
        "step": [
          {
            "@type": "HowToStep",
            "name": "Choose your jar size",
            "text": "Select a preset jar size (120, 200, or 300 ml) or enter a custom volume in milliliters"
          },
          {
            "@type": "HowToStep",
            "name": "Enter batch quantity",
            "text": "Enter the number of candles in your batch to calculate total material needs"
          },
          {
            "@type": "HowToStep",
            "name": "Get your results",
            "text": "The calculator instantly shows the dry wax and fragrance oil needed per candle and for the entire batch"
          }
        ]
      }
    ]
  };
</script>

<svelte:head>
  <title>Candle Wax & Fragrance Calculator — Candle Lab | Free Online Tool</title>
  <meta name="description" content="Free online candle making calculator. Calculate how much wax and fragrance oil you need for any jar size. Supports soy wax, paraffin, coconut wax. Batch calculation with popular jar presets." />
  <meta name="keywords" content="candle calculator, candle wax calculator, candle making calculator, fragrance oil calculator, how much wax for candle, wax calculator, candle batch calculator, soy wax calculator, candle supply calculator, DIY candle calculator" />
  <link rel="canonical" href="{siteUrl}/en/" />
  <link rel="alternate" hreflang="ru" href="{siteUrl}/" />
  <link rel="alternate" hreflang="en" href="{siteUrl}/en/" />
  <link rel="alternate" hreflang="x-default" href="{siteUrl}/" />

  <!-- Open Graph -->
  <meta property="og:type" content="website" />
  <meta property="og:title" content="Candle Wax & Fragrance Calculator — Candle Lab" />
  <meta property="og:description" content="Free online candle making calculator. Calculate how much wax and fragrance oil you need for any jar size." />
  <meta property="og:url" content="{siteUrl}/en/" />
  <meta property="og:site_name" content="Candle Lab" />
  <meta property="og:locale" content="en_US" />
  <meta property="og:locale:alternate" content="ru_RU" />

  <!-- Twitter Card -->
  <meta name="twitter:card" content="summary" />
  <meta name="twitter:title" content="Candle Wax & Fragrance Calculator — Candle Lab" />
  <meta name="twitter:description" content="Free online candle making calculator. Calculate how much wax and fragrance oil you need for any jar size." />

  <!-- JSON-LD Structured Data -->
  {@html `<script type="application/ld+json">${JSON.stringify(jsonLd)}</script>`}
</svelte:head>

<main class="page" lang="en">
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
      <nav class="panel-actions" aria-label="Language selection">
        <div class="language-toggle" role="group" aria-label={t.languageLabel}>
          <span class="language-label">{t.languageLabel}</span>
          <div class="toggle-buttons">
            <a href="/">RU</a>
            <a href="/en/" class="active" aria-current="page">EN</a>
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

  <section class="seo-content" aria-label="About the calculator">
    <h2>{t.aboutTitle}</h2>
    <p>{t.aboutText}</p>
  </section>

  <section class="faq" aria-label="Frequently Asked Questions" itemscope itemtype="https://schema.org/FAQPage">
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
