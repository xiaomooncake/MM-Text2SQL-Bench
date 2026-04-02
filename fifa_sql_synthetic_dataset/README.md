# FIFA 2017 Synthetic NL2SQL Dataset

This package contains a large automatically generated Text-to-SQL style dataset built from the FIFA 2017 player dataset schema.

## Included files

- `data/fifa_nl2sql_synthetic.jsonl`: main dataset in JSONL format
- `data/fifa_nl2sql_synthetic.csv`: same content in CSV format
- `data/train.jsonl`, `data/dev.jsonl`, `data/test.jsonl`: simple random split
- `database/schema.sql`: database schema
- `docs/metadata.json`: dataset statistics

## Fields

Each example contains:

- `id`
- `question`
- `gold_sql`
- `database_schema`
- `template`
- `difficulty`
- `source`

## Statistics

- Total examples: 4138
- Train: 3310
- Dev: 414
- Test: 414

## Important note

These samples were generated automatically from schema-aware templates. The user explicitly allowed that the content can be temporarily imperfect, so the current version emphasizes quantity and structure over strict SQL correctness.
