# CS 4200 Final Project: JobFit Pipeline

An automated job-matching pipeline that scrapes listings from Indeed, scores them against a user-provided resume using natural language processing, and exports a ranked report of the best-fit opportunities.

## What It Does

1. **Scrapes** job listings from Indeed based on a configurable search query and location.
2. **Stores** results in MongoDB to simulate real-world data persistence.
3. **Cleans** each job description by removing boilerplate (EEO statements, benefits sections, "about us" text) so only the relevant content is scored.
4. **Scores** each listing by comparing its description to the resume using sentence-transformer embeddings and cosine similarity.
5. **Filters** out listings that require substantially more experience than the resume reflects, using date-parsed resume sections to measure relevant years on a per-job basis.
6. **Ranks and exports** the results to a single CSV that overwrites on each run, ready for downstream automation.

## Why It Exists

This project demonstrates an end-to-end workflow that mirrors the structure of a production-scale job matching system. The pipeline — ingest, store, embed, score, rank, serve — is the same pattern used by enterprise platforms at much larger volumes. Migrating to a cloud data warehouse like Snowflake would scale each step horizontally without changing the underlying logic. This is a small-scale demonstration of a big-scale process.

## Tech Stack

- **Python** (Playwright, Playwright Stealth, Motor, PyMuPDF, sentence-transformers, scikit-learn)
- **MongoDB** (via MongoDB Atlas) for document storage
- **Quarto** for the development notebook

## Getting Started

1. Clone the repo and install dependencies (see the pip install cell at the top of the `.qmd` file).
2. Update the MongoDB connection string, search parameters, and resume path in the config cells.
3. Place the resume PDF at the configured path.
4. Run the notebook top to bottom.

Output is written to `job_match_report.csv` in the project directory.

## Future Roadmap

- Scheduled recurring runs
- Email/text notifications for high-scoring matches
- Historical tracking alongside the current-snapshot CSV
- Migration path to a cloud data warehouse for scale

## Notes

Full project documentation, including methodology and AI assistance disclosure, is available in the Quarto notebook.