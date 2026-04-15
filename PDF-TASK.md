# PDF Generation Task — Fantasy iGaming Data Department

## Цель

Собрать весь контент сайта (19 HTML-страниц) в один PDF-документ формата книги. 80-120 страниц, профессиональная вёрстка, оглавление, нумерация страниц. PDF — offline-версия сайта для скачивания и шаринга.

## Источники контента

Контент берётся из HTML-файлов в папке `pages/`:

| # | Файл | Глава PDF |
|---|------|-----------|
| — | index.html | Обложка + вступление (company card) |
| 01 | data-architecture.html | Глава 1: Data Architecture |
| 02 | org-structure.html | Глава 2: Org Structure |
| 03 | data-model.html | Глава 3: Data Model |
| 04 | event-taxonomy.html | Глава 4: Event Taxonomy |
| 05 | metrics.html | Глава 5: Metrics Dictionary |
| 06 | data-governance.html | Глава 6: Data Governance |
| 07 | sla.html | Глава 7: SLA |
| 08 | dataops.html | Глава 8: DataOps |
| 09 | mlops.html | Глава 9: MLOps |
| 10 | data-lineage.html | Глава 10: Data Lineage |
| 11 | incident-response.html | Глава 11: Incident Response |
| 12 | dashboards.html | Глава 12: Dashboard Mockups |
| 13 | ab-testing.html | Глава 13: A/B Testing Framework |
| 14 | management.html | Глава 14: Management Practices |
| 15 | onboarding.html | Глава 15: Onboarding Guide |
| 16 | finops.html | Глава 16: FinOps |
| 17 | roadmap.html | Глава 17: Annual Roadmap |
| 18 | glossary.html | Приложение A: Glossary |
| 19 | about.html | Послесловие: О проекте и авторе |

## Структура PDF

### Обложка (страница 1)
- Заголовок: **Fantasy iGaming Data Department**
- Подзаголовок: **The Ultimate Data Function Reference**
- Описание: "Полный playbook по организации аналитической функции в iGaming-компании"
- Год: 2026
- Автор: Константин Гупалов
- Визуал: минималистичный, тёмный фон (как сайт), accent purple

### Страница 2 — Disclaimer
"Все данные, компании и структуры вымышлены. Это не best practice и не консалтинг. Стартовая точка для обсуждения и обучения."

### Страница 3-4 — Оглавление
Автоматически сгенерированное, с номерами страниц.
Три уровня: Глава → Секция → Подсекция.

### Страница 5 — О компании
Company card из index.html: продукт, рынки, MAU, NGR, команда, стадия, стек.

### Главы 1-17 — основной контент
Каждая глава = одна страница сайта. Начинается с новой страницы.

### Приложение A — Glossary
Алфавитный список терминов.

### Послесловие — О проекте и авторе
Из about.html.

## Правила вёрстки

### Общие
- Формат: A4 portrait
- Поля: top 25mm, bottom 25mm, left 30mm, right 20mm
- Шрифты: основной текст — sans-serif (аналог DM Sans), код — monospace (аналог JetBrains Mono)
- Размер: основной текст 11pt, заголовки глав 18pt, секций 14pt, подсекций 12pt
- Межстрочный интервал: 1.4
- Нумерация страниц: внизу по центру, начиная с оглавления

### Заголовки глав
- Каждая глава начинается с новой страницы
- Номер главы + название: "01. Data Architecture"
- Под заголовком: краткое описание (page-header-desc из HTML)
- Горизонтальная линия-разделитель

### Таблицы
- Все таблицы из HTML переносятся как есть
- Альтернирующие строки (зебра) для читаемости
- Если таблица не помещается на страницу — разрыв с повтором заголовка
- Conditional formatting (цветные бейджи) — заменить на текстовые маркеры: [OK], [WARN], [ALERT] или (expert), (proficient), (basic)

### Code blocks
- Фон: светло-серый (#f5f5f0)
- Шрифт: monospace, 9pt
- Рамка: тонкая, 0.5pt
- Язык указан над блоком: SQL, Python, YAML, JSON
- Подсветка синтаксиса: keywords bold, strings в кавычках, comments italic серым

### Alert boxes
- Заменить цветные плашки на:
  - TIP: иконка "✓" + серая рамка слева
  - WARNING: иконка "⚠" + серая рамка слева
  - INFO: иконка "ℹ" + серая рамка слева

### Mermaid-диаграммы
- ERD (data-model.html): предварительно отрендерить mermaid → PNG/SVG, вставить как изображение
- Flowcharts (data-lineage.html): аналогично → PNG/SVG
- Если рендеринг невозможен: заменить на текстовое описание в виде ASCII-схемы

### Dashboard mockups (глава 12)
- KPI-карточки: отрисовать как таблицу (метрика | значение | WoW)
- Графики (sparklines, bar charts): описать текстом или упрощённой ASCII-таблицей
- Heatmap: таблица с числами, без цветов (цвета не передаются в ч/б печати)

### Onboarding checklist (глава 15)
- Чекбоксы: заменить на ☐ (пустой квадрат), пригодный для печати и заполнения вручную

### Ссылки
- Внутренние ссылки между страницами → "см. Главу N, секция X"
- Внешние ссылки → полный URL в сноске или в скобках

## Workflow

1. Прочитать SKILL.md для PDF-генерации: `/mnt/skills/public/pdf/SKILL.md`
2. Извлечь текстовый контент из каждого HTML-файла в pages/ (парсить HTML, убрать навигацию/sidebar/footer, оставить контент)
3. Для mermaid-диаграмм: попытаться отрендерить в PNG через CLI или заменить на текстовые описания
4. Собрать всё в единый документ с правильной структурой
5. Сгенерировать PDF
6. Сохранить в `/mnt/user-data/outputs/fantasy-igaming-data-department.pdf`

## Имя выходного файла

`Fantasy_iGaming_Data_Department_Playbook_2026.pdf`

## Ожидаемый объём

80-120 страниц A4. Если получается меньше 70 — контент потерялся. Если больше 150 — слишком много whitespace.
