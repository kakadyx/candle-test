<script>
  import { flip } from 'svelte/animate';
  import { cubicOut } from 'svelte/easing';
  import { fly } from 'svelte/transition';

  export let language = 'ru';

  const WAX_DENSITY = 0.925;
  const FRAGRANCE_RATIO = 0.05;

  const translations = {
    ru: {
      eyebrow: 'Candle Lab',
      heroTitle: 'Калькулятор воска и отдушки для свечей',
      heroLead:
        'Бесплатный онлайн-калькулятор для расчёта воска и отдушки при изготовлении свечей. Добавляйте несколько калькуляторов, чтобы сравнивать разные объёмы баночек.',
      addCalculator: 'Добавить калькулятор',
      formulaTitle: 'Формулы',
      formulaWax: 'Сухой воск = объем x 0.925',
      formulaFragrance: 'Отдушка = сухой воск x 0.05',
      panelLabel: 'Формулы и коэффициенты',
      ratiosTitle: 'Коэффициенты',
      waxShareLabel: 'доля воска (от объема банки)',
      fragranceShareLabel: 'доля отдушки (от объема сухого воска)',
      panelNote: 'Меняйте значения под объём банки и размер партии.',
      batchLabel: 'Партия',
      cardTitle: 'Объём банки и количество свечей',
      remove: 'Удалить',
      presetsLabel: 'Пресеты баночек',
      jarVolume: 'Объём банки (мл)',
      candleCount: 'Количество свечей',
      jarPlaceholder: 'например, 220',
      countPlaceholder: 'например, 6',
      waxPerLabel: 'Сухой воск на 1 свечу',
      fragrancePerLabel: 'Отдушка на 1 свечу',
      totalShort: 'Всего',
      ml: 'мл',
      gramShort: 'г',
      languageLabel: 'Язык',
    },
    en: {
      eyebrow: 'Candle Lab',
      heroTitle: 'Candle Wax & Fragrance Calculator',
      heroLead:
        'Free online candle making calculator. Calculate wax and fragrance oil needed for any jar size. Add multiple calculators to compare jar sizes side by side.',
      addCalculator: 'Add calculator',
      formulaTitle: 'Formulas',
      formulaWax: 'Dry wax = volume x 0.925',
      formulaFragrance: 'Fragrance = dry wax x 0.05',
      panelLabel: 'Formulas & ratios',
      ratiosTitle: 'Ratios',
      waxShareLabel: 'wax share (of jar volume)',
      fragranceShareLabel: 'fragrance share (of dry wax)',
      panelNote: 'Adjust values to match your jar volume and batch size.',
      batchLabel: 'Batch',
      cardTitle: 'Jar volume + candle count',
      remove: 'Remove',
      presetsLabel: 'Jar presets',
      jarVolume: 'Jar volume (ml)',
      candleCount: 'Number of candles',
      jarPlaceholder: 'e.g. 220',
      countPlaceholder: 'e.g. 6',
      waxPerLabel: 'Dry wax per candle',
      fragrancePerLabel: 'Fragrance per candle',
      totalShort: 'Total',
      ml: 'ml',
      gramShort: 'g',
      languageLabel: 'Language',
    },
  };

  const PREPOSITION_REGEX =
    /(^|[\s\u00A0"\u00AB(])(в|к|с|о|у|из|от|на|по|за|под|над|для|и|а|но|да|не|ни|же|ли)\s+/giu;

  const fixPrepositions = (text) => text.replace(PREPOSITION_REGEX, '$1$2\u00A0');

  const localize = (lang) => {
    const strings = translations[lang];
    if (lang !== 'ru') {
      return strings;
    }
    const localized = {};
    for (const key in strings) {
      if (Object.prototype.hasOwnProperty.call(strings, key)) {
        localized[key] = fixPrepositions(strings[key]);
      }
    }
    return localized;
  };

  const presetOptions = [
    { key: 'manual', labels: { ru: 'Вручную', en: 'Manual' }, volume: null },
    { key: 'small', labels: { ru: 'Маленькая', en: 'Small' }, volume: 120 },
    { key: 'medium', labels: { ru: 'Средняя', en: 'Medium' }, volume: 200 },
    { key: 'large', labels: { ru: 'Большая', en: 'Large' }, volume: 300 },
  ];

  let nextId = 1;
  const createId = () => `calc-${nextId++}`;

  const createCalculator = (overrides = {}) => ({
    id: createId(),
    volumeMl: '200',
    count: '1',
    preset: 'manual',
    ...overrides,
  });

  let calculators = [createCalculator()];
  let numberFormatter;
  let plainFormatter;

  $: t = localize(language);
  $: numberFormatter = new Intl.NumberFormat(language === 'ru' ? 'ru-RU' : 'en-US', {
    minimumFractionDigits: 2,
    maximumFractionDigits: 2,
  });
  $: plainFormatter = new Intl.NumberFormat(language === 'ru' ? 'ru-RU' : 'en-US', {
    maximumFractionDigits: 2,
  });

  const addCalculator = () => {
    calculators = [...calculators, createCalculator()];
  };

  const removeCalculator = (id) => {
    calculators = calculators.filter((calc) => calc.id !== id);
  };

  const updateCalculator = (id, changes) => {
    calculators = calculators.map((calc) =>
      calc.id === id ? { ...calc, ...changes } : calc
    );
  };

  const selectPreset = (id, option) => {
    if (option.key === 'manual') {
      updateCalculator(id, { preset: 'manual' });
      return;
    }
    updateCalculator(id, {
      preset: option.key,
      volumeMl: String(option.volume),
    });
  };

  const parsePositive = (value) => {
    const num = parseFloat(value);
    if (!Number.isFinite(num) || num <= 0) {
      return null;
    }
    return num;
  };

  const computeTotals = (calc) => {
    const volume = parsePositive(calc.volumeMl);
    const count = parsePositive(calc.count);

    const waxPer = volume ? volume * WAX_DENSITY : null;
    const fragrancePer = waxPer ? waxPer * FRAGRANCE_RATIO : null;

    return {
      volume,
      count,
      waxPer,
      fragrancePer,
      waxTotal: waxPer && count ? waxPer * count : null,
      fragranceTotal: fragrancePer && count ? fragrancePer * count : null,
    };
  };

  const formatValue = (value) => {
    if (value === null) {
      return '--';
    }
    return numberFormatter.format(value);
  };

  const formatPlain = (value) => {
    if (value === null) {
      return '--';
    }
    return plainFormatter.format(value);
  };
</script>

<div class="cards-header">
  <h2 class="cards-title">{t.panelNote}</h2>
  <button class="primary" type="button" on:click={addCalculator}>
    {t.addCalculator}
  </button>
</div>

<section class="cards">
  {#each calculators as calc, index (calc.id)}
    {@const totals = computeTotals(calc)}
    {@const showTotals = totals.count && totals.count > 1}
    <article
      class="calc-card"
      in:fly={{ y: 28, duration: 520, delay: index * 90, easing: cubicOut }}
      out:fly={{ y: 18, duration: 260, easing: cubicOut }}
      animate:flip={{ duration: 320, easing: cubicOut }}
    >
      <div class="card-head">
        <div>
          <p class="card-eyebrow">{t.batchLabel} {index + 1}</p>
          <h2 class="card-title">{t.cardTitle}</h2>
        </div>
        {#if calculators.length > 1}
          <button class="ghost" type="button" on:click={() => removeCalculator(calc.id)}>
            {t.remove}
          </button>
        {/if}
      </div>

      <div class="preset-block">
        <span class="preset-label">{t.presetsLabel}</span>
        <div class="preset-buttons">
          {#each presetOptions as option}
            <button
              type="button"
              class:active={calc.preset === option.key}
              on:click={() => selectPreset(calc.id, option)}
            >
              <span>{option.labels[language]}</span>
              {#if option.volume}
                <span class="preset-volume">{option.volume} {t.ml}</span>
              {/if}
            </button>
          {/each}
        </div>
      </div>

      <div class="inputs">
        <label class="field">
          <span>{t.jarVolume}</span>
          <input
            type="number"
            min="1"
            step="1"
            placeholder={t.jarPlaceholder}
            value={calc.volumeMl}
            on:input={(event) =>
              updateCalculator(calc.id, {
                volumeMl: event.currentTarget.value,
                preset: 'manual',
              })
            }
          />
        </label>
        <label class="field">
          <span>{t.candleCount}</span>
          <input
            type="number"
            min="1"
            step="1"
            placeholder={t.countPlaceholder}
            value={calc.count}
            on:input={(event) =>
              updateCalculator(calc.id, { count: event.currentTarget.value })
            }
          />
        </label>
      </div>

      <div class="summary">
        <div class="summary-row">
          <span class="summary-label">{t.jarVolume}</span>
          <span class="summary-value">
            <span class="summary-per">{formatPlain(totals.volume)} {t.ml}</span>
          </span>
        </div>
        <div class="summary-row">
          <span class="summary-label">{t.candleCount}</span>
          <span class="summary-value">
            <span class="summary-per">{formatPlain(totals.count)}</span>
          </span>
        </div>
        <div class="summary-row">
          <span class="summary-label">{t.waxPerLabel}</span>
          <span class="summary-value">
            <span class="summary-per">{formatValue(totals.waxPer)} {t.gramShort}</span>
            {#if showTotals}
              <span class="summary-total">
                {t.totalShort}: {formatValue(totals.waxTotal)} {t.gramShort}
              </span>
            {/if}
          </span>
        </div>
        <div class="summary-row">
          <span class="summary-label">{t.fragrancePerLabel}</span>
          <span class="summary-value">
            <span class="summary-per">
              {formatValue(totals.fragrancePer)} {t.gramShort}
            </span>
            {#if showTotals}
              <span class="summary-total">
                {t.totalShort}: {formatValue(totals.fragranceTotal)} {t.gramShort}
              </span>
            {/if}
          </span>
        </div>
      </div>
    </article>
  {/each}
</section>
