# Recruitment Intelligence Pipeline

A Python ETL project that collects job postings from five job-board sources, normalizes them into a shared record, enriches selected fields, removes duplicates, and writes analysis-ready outputs.

## Workflow

1. **Extract.** Source adapters query Reed, Adzuna, The Muse, Remotive, and Arbeitnow using configured keywords and source-specific pagination.
2. **Normalize.** `utils.py` provides the shared `JobPosting` model and helpers for dates, salaries, skills, polite request pacing, and optional geocoding.
3. **Combine and deduplicate.** `pipeline.py` orchestrates the adapters, applies a cross-source fingerprint, and consolidates the collected postings.
4. **Export.** Each run writes structured CSV and JSON files plus a human-readable briefing under `output/`.
5. **Schedule (optional).** `scheduler.py` runs the pipeline repeatedly and writes rotating logs.

The pipeline includes support for searches across 16 Adzuna country codes. Geocoding can be disabled with `--no-geo`. Source APIs have their own rate limits and may require credentials; configure credentials through environment variables and keep them out of version control.

## Repository structure

```text
Jobs Project/
├── README.md
├── PROJECT_OVERVIEW.md
├── User Guide — Recruitment Scraper.md
├── Data Description — Recruitment Scraper.md
├── pipeline.py
├── scheduler.py
├── utils.py
├── reed_scraper.py
├── adzuna_scraper.py
├── themuse_scraper.py
├── remotive_scraper.py
├── arbeitnow_scraper.py
├── requirements.txt
├── Dockerfile
├── docker-compose.yml
├── output/                 # sample exports are tracked; new runs write here
└── logs/                   # created by the scheduler at runtime
```

## Run it

Use Python 3.10 or later.

```bash
python -m pip install -r requirements.txt
python pipeline.py
```

A smaller, faster run can skip geocoding:

```bash
python pipeline.py --keywords "Data Analyst,DevOps Engineer" --countries us,gb --no-geo
```

To run the scheduled collector:

```bash
python scheduler.py --interval 12
```

For operating details and the output schema, see the [user guide](<User Guide — Recruitment Scraper.md>) and [data description](<Data Description — Recruitment Scraper.md>). See the [project overview](PROJECT_OVERVIEW.md) for coverage, fields, and analysis use cases.
