Update the ETA victims database JS array from a CSV export.

## What this does
Reads the ETA victims CSV file, converts it to the JS array format, and overwrites `static/database/eta_js_array.txt`.

## Steps

1. Identify the CSV path. The user will typically provide it (e.g. `"C:\Users\kathr\OneDrive\Book\App\ETA Victims list v0.12.csv"`). If not provided, look for the most recently modified CSV matching `C:\Users\kathr\OneDrive\Book\App\ETA Victims list*.csv`.

2. Run this Python script via the Bash tool to convert the CSV and write the output file:

```python
import csv, json

csv_path = r"REPLACE_WITH_CSV_PATH"
out_path = r"C:\Users\kathr\Projects\kloosemore.github.io\static\database\eta_js_array.txt"

rows = []
with open(csv_path, 'rb') as _f:
    _bom = _f.read(3)
_enc = 'utf-8-sig' if _bom == b'\xef\xbb\xbf' else 'latin-1'
with open(csv_path, newline='', encoding=_enc) as f:
    reader = csv.DictReader(f)
    for row in reader:
        def num(val, default=0):
            v = val.strip() if val else ''
            return int(v) if v.lstrip('-').isdigit() else default

        def s(val):
            return (val or '').strip()

        day_raw = s(row.get('DAY', ''))
        day = int(day_raw) if day_raw.isdigit() else ''

        obj = {
            "day": day,
            "month": s(row.get('MONTH', '')),
            "year": num(row.get('YEAR', ''), 0),
            "kidnapped": num(row.get('KIDNAPPED', ''), 0),
            "murdered": num(row.get('MURDERED', ''), 0),
            "injured": num(row.get('INJURED', ''), 0),
            "victims": num(row.get('VICTIMS', ''), 0),
            "target": s(row.get('VICTIMS/TARGET', '')),
            "method": s(row.get('METHOD', '')),
            "context": s(row.get('CONTEXTUAL INFORMATION', '')),
            "location": s(row.get('LOCATION', '')),
            "source": s(row.get('Source', '')),
            "source2": s(row.get('ADDITIONAL SOURCE', '')),
            "source3": s(row.get('ADDITIONAL SOURCE 2', '')),
            "source4": s(row.get('ADDITIONAL SOURCE 3', '')),
            "reaction": s(row.get('REACTION', '')),
            "warning": s(row.get('WARNING GIVEN', '')),
        }
        rows.append(obj)

with open(out_path, 'w', encoding='utf-8') as f:
    f.write('const etaData = [\n')
    for i, obj in enumerate(rows):
        parts = [f'"{k}": {json.dumps(v, ensure_ascii=False)}' for k, v in obj.items()]
        line = '{' + ', '.join(parts) + '}'
        f.write(line + (',' if i < len(rows) - 1 else '') + '\n')
    f.write('];\n')

print(f"Written {len(rows)} rows to {out_path}")
```

3. Report back: how many rows were written, and confirm the first and last rows look correct by reading lines 1–3 and the last 2 lines of the output file.

4. Build the site by running `hugo` via Bash.

5. Stage and commit both the source and built files, then push:
   ```
   git add static/database/eta_js_array.txt public/
   git commit -m "data: update ETA victims database to vX.XX"
   git push origin main
   ```

## CSV column mapping
| CSV column | JS field |
|---|---|
| DAY | day (int, or "" if blank) |
| MONTH | month |
| YEAR | year |
| KIDNAPPED | kidnapped (0 if blank) |
| MURDERED | murdered (0 if blank) |
| INJURED | injured (0 if blank) |
| VICTIMS | victims (0 if blank) |
| VICTIMS/TARGET | target |
| METHOD | method |
| CONTEXTUAL INFORMATION | context |
| LOCATION | location |
| Source | source |
| ADDITIONAL SOURCE | source2 |
| ADDITIONAL SOURCE 2 | source3 |
| ADDITIONAL SOURCE 3 | source4 |
| REACTION | reaction |
| WARNING GIVEN | warning |
