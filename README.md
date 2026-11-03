# Infinity Paper Library

Research Paper Content Enrichment, by Jonella (Infinity operations). Tests of making the actual written content of graduates' research papers searchable by topic or keyword, not just their Google Scholar or OpenAlex profile links.

**Live pages**
- Paper Library: search titles, abstracts and keywords of 4,073 papers from 297 graduate candidates (`index.html`)
- Full Text Test: search inside the full text of 125 papers from 21 tech candidates, compared with searching summaries only (`fulltext/index.html`)

The layout and search rules follow Eloisa's [Infinity Research Library](https://eloisa-cpu.github.io/infinity-research-library-v2/), so the two can be combined later.

## What's in it

| Test | People | Papers | What is searched |
|---|---|---|---|
| Pilot 1 (mixed departments) | 150 | 2,479 | Titles, abstracts, topics, keywords |
| Pilot 2 (CS, EE, Physics only) | 150 | 1,808 | Titles, abstracts, topics, keywords |
| Paper Library (both pilots, duplicates merged) | 297 | 4,073 | Titles, abstracts, topics, keywords |
| Full Text Test (from Pilot 2) | 21 | 125 | Whole paper, split into ~130-word passages with page numbers |

Schools: Harvard, Princeton, UC Berkeley, Caltech, MIT, Stanford (about 25 per school per pilot).

Each candidate has an Infinity fit rating (Strong, Possible, No clear fit) and a possible role, matched by hand from their papers to the Roles tab in the pilot sheets. These are a first read, not a final assessment.

## Search rules

Words must all appear (any order). `"exact phrase"` · `CUDA OR Triton` · `-exclude` · `quantiz*` for word starts. Not case-sensitive.

## Findings so far

- Focusing on technical departments works better: No clear fit dropped from 99 of 150 (mixed) to 35 of 150 (CS, EE, Physics).
- Full text finds people that summaries miss, especially for tools and hardware:

| Search | Summaries only | Full paper text |
|---|---|---|
| GPU | 4 people | 12 people |
| throughput | 0 | 11 |
| PyTorch | 1 | 9 |
| H100 OR A100 | 0 | 7 |
| kernel | 1 | 14 |

Some full-text matches are passing mentions (for example a thank-you note), so the page shows the exact passage and page number for checking.

## Data sources

- [OpenAlex](https://openalex.org) API for paper lists, titles, abstracts, topics and keywords (about $0.015 for pilot 2 on the free daily budget).
- Google Scholar profile lists from the graduate sheets (pilot 1).
- Full text: free PDFs from arXiv and open-access links found through OpenAlex. Reference lists are left out. 34 of 159 papers could not be downloaded (publisher blocked or no free copy).

## Files

- `index.html`, `data.json`: Paper Library page and its data
- `fulltext/index.html`, `fulltext/ft_data.json`: Full Text Test page and its data
- `scripts/`: Python scripts used to pick people, pull OpenAlex data, assign fit and role, download PDFs and extract text
  - `pick2.py`, `fetch2.py`, `build2.py`, `role_map.py`, `role_map2.py`: pilot data and fit ratings
  - `build_data.py`: merges both pilots into `data.json`
  - `pick_ft.py`, `download.py`, `extract.py`: full-text test (also builds a SQLite full-text database)

PDFs are not included in this repository.

## Next steps

- Decide whether to run all ~17,000 graduates or only technical departments.
- OpenAlex credits for the full run (about $7 to $10).
- Move storage to a database for the full run (the full-text test alone is about 1.3 million words for 125 papers).
- Agree on one shared format with Eloisa so papers and blog posts can be searched together.
