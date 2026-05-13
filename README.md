# General Data Cleaner

Automatically clean CSV, Excel, and JSON files with full audit trails, PII masking, and budget control. Remove duplicates, fix missing values, standardize dates and numbers, and get quality reports — all in one step.

## Why use this Actor?

- Save time – Stop manually fixing spreadsheets. Let the cleaner handle missing values, duplicates, outliers, and format inconsistencies.
- Audit ready – Every change is logged. You get task-level and rule-level CSV reports, plus an HTML quality report with ISO 8000 scores.
- Privacy safe – Enable PII masking to automatically redact SSNs, credit card numbers, and emails (irreversible).
- Cost control – Set your budget limit; the Actor stops when reached (hard cap $10.00).
- Preview mode – Test with first N rows before cleaning your full dataset.

## Input Parameters (JSON)

Provide input as a JSON object. Example:

{
  "sourceData": "https://example.com/my-data.csv",
  "delimiter": "auto",
  "encoding": "auto",
  "auditLevel": "rule",
  "maxChargeUsd": 5.0,
  "previewMode": false,
  "previewRows": 100,
  "enablePiiMasking": false,
  "piiMaskingRules": "",
  "cellErrorPolicy": "skip_cell",
  "outputFormat": "csv",
  "locale": "US"
}

### Parameter reference

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| sourceData | string | Yes | – | URL, local path, or Apify Dataset ID (e.g., dataset-username/dataset-name) of the input file. Supports CSV, Excel (.xlsx, .xls), JSON. |
| delimiter | string | No | auto | Column delimiter: auto (detect), ",", ";", "\t", "|". |
| encoding | string | No | auto | File encoding: auto (detect), "utf-8", "iso-8859-1", etc. |
| auditLevel | string | No | rule | Audit granularity: "task" (only run summary) or "rule" (per cleaning rule). |
| maxChargeUsd | number | No | 5.0 | Budget limit (USD). Actual stop = min(this, system hard cap $10.0). |
| previewMode | boolean | No | false | If true, only process first previewRows. |
| previewRows | integer | No | 100 | Number of rows to process when previewMode=true (max 10,000). |
| enablePiiMasking | boolean | No | false | If true, mask SSN, credit cards, emails (irreversible). |
| piiMaskingRules | string | No | "" | Comma-separated column names or regex patterns for additional masking (e.g., "phone,custom_id"). |
| cellErrorPolicy | string | No | skip_cell | How to handle cell conversion errors: "skip_cell" (keep original, continue) or "stop_rule" (fail the rule). |
| outputFormat | string | No | csv | Output format: "csv", "excel", or "json". |
| locale | string | No | US | Date and number format: "US" (MM/DD/YYYY, 1,234.56) or "EU" (DD/MM/YYYY, 1.234,56). |

## Output Files

After a successful run, you will find the following files:

| File | Location | Description |
|------|----------|-------------|
| Cleaned data | Apify Dataset | The cleaned dataset in your chosen format (CSV/Excel/JSON). |
| Task audit | Key-Value Store → audit_task_{{run.id}}.csv | One row per run: session_id, timestamps, exit reason, budget used, preview mode flag. |
| Rule audit | Key-Value Store → audit_rules_{{run.id}}.csv | One row per cleaning rule: rule_id, affected rows, execution time, status (only when auditLevel=rule). |
| Skipped rows | Key-Value Store → audit_skipped_{{run.id}}.csv | Rows that could not be parsed (e.g., encoding errors, column mismatches). |
| Quality report (HTML) | Key-Value Store → quality_report_{{run.id}}.html | Human‑readable report with ISO 8000 dimension scores (completeness, accuracy, consistency, format). |
| Quality report (JSON) | Key-Value Store → quality_report_{{run.id}}.json | Same data in JSON format. |
| Error report | Key-Value Store → errors_{{run.id}}.json | Detailed error information (if any). |
| Debug log | Key-Value Store → debug_log_{{run.id}}.txt | Last 1000 log lines (saved only if an error occurs). |

> Tip: The first record in the Dataset is an OUTPUT_SUMMARY that lists all the above keys. You can also access the Key-Value Store directly via the Apify Console.

## Usage Examples

### 1. Basic cleaning (run with defaults)
If you set a default sourceData (e.g., our example CSV), simply click Run with defaults. The Actor will clean the example file and output the results.

### 2. Clean your own file from a URL
Set sourceData to the URL of your CSV/Excel/JSON file.

### 3. Preview mode (test before full run)
Set previewMode to true and previewRows to e.g. 100.

### 4. Enable PII masking
Set enablePiiMasking to true and optionally piiMaskingRules.

### 5. European locale (EU)
Set locale to "EU" and delimiter to ";" if needed.

## How to Use (Apify Console)

1. Go to the Actor page.
2. In the Input tab, switch to JSON mode (or use the form).
3. Paste your JSON configuration (see examples above).
4. Click Start.
5. Download the cleaned dataset from the Dataset tab, and audit/quality reports from the Key-Value Store.

## Bugs, fixes, updates, and changelog

This product is under active development. If you encounter any issues, have feature requests, or would like to provide feedback, please open an issue on our GitHub repository:

👉 [here](https://github.com/yuliu-digitaltwin/apify-lunar-data-cleaner/issues)

## Support

Email: liuyu.digitaltwin@outlook.com
Please include your session_id (found in the Actor run log or task audit CSV) when reporting issues.

## License

MIT