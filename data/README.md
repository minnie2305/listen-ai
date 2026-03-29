# Data Folder

This folder contains the SQLite database and helper script for importing post data.

## Files

- `listenai.db`: SQLite database file.
- `import_posts.py`: Download CSV (optional) and import rows into `posts` table.

## CSV Format

The CSV file must have exactly 3 columns:

```csv
name,date,content
```

Date format must be:

```text
YYYY-MM-DD
```

## Install gdown (for Google Drive download)

```bash
pip install gdown
```

## Placeholder Google Drive Link

Replace this placeholder with your actual file URL when ready:

```text
https://drive.google.com/uc?id=YOUR_GOOGLE_DRIVE_FILE_ID
```

## Usage

Run from project root:

```bash
python data/import_posts.py --csv ./posts.csv --db ./data/listenai.db
```

Download with `gdown` first, then import:

```bash
python data/import_posts.py \
  --download \
  --drive-url "https://drive.google.com/uc?id=YOUR_GOOGLE_DRIVE_FILE_ID" \
  --csv ./posts.csv \
  --db ./data/listenai.db
```

Optional platform override (default is `x`):

```bash
python data/import_posts.py --platform reddit
```

## Behavior

- Creates `posts` table if missing.
- Maps:
  - `name` -> `author`
  - `date` -> `created_at` (stored as `YYYY-MM-DDT00:00:00Z`)
  - `content` -> `content`
- Skips duplicate rows (same `author`, `content`, and `created_at`).
- Prints summary with inserted/skipped/bad row counts.
