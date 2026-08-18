# Dynamic ETL - Data Dictionary

## 1. Consolidated model output

| Field | Type | Nullable | Source / rule |
|---|---|---:|---|
| `Date` | date | No | Logical business run date |
| `Ticker` | string | No | Parsed from source workbook filename using documented naming rule |
| `Type` | string | Yes | Model type from sheet naming rule; NULL when absent |
| `Quarter` | integer/string | No | Regression Model period field after schema validation |
| `Year` | integer | No | Regression Model period field after schema validation |
| `Estimated Total Sold` | decimal | No* | Empirical Model labeled value |
| `Estimated Sold Max` | decimal | No* | Empirical Model labeled value |
| `Estimated Sold Min` | decimal | No* | Empirical Model labeled value |
| `Forecast w/o SA Actual` | decimal | No* | Regression Model labeled value |
| `Forecast w/o SA Max` | decimal | No* | Regression Model labeled value |
| `Forecast w/o SA Min` | decimal | No* | Regression Model labeled value |

`*` Nullability must be decided from real business data. Missing mandatory values must not silently become zero.

## 2. Datasheet target

Legacy target fields:

| Field | Suggested logical type |
|---|---|
| `Date` | date |
| `FacilityType` | string |
| `BedSize` | integer/string depending on source semantics |
| `Region` | string |
| `Manufacturer` | string |
| `Ticker` | string |
| `Group` | string |
| `Therapy` | string |
| `Anatomy` | string |
| `SubAnatomy` | string |
| `ProductCategory` | string |
| `Quantity` | decimal/integer |
| `AvgPrice` | decimal |
| `TotalSpend` | decimal |

The implementation team must validate source formats rather than infer types from names alone.

## 3. Run metadata

Recommended fields:

- `run_id`
- `business_date`
- `source_archive_name`
- `source_archive_sha256`
- `ingested_at`
- `started_at`
- `completed_at`
- `status`
- `files_discovered`
- `files_processed`
- `records_model`
- `records_datasheet`
- `records_rejected`
- `application_version`
- `schema_version`

## 4. Data-quality rules

At minimum validate:

- ticker can be derived;
- Empirical/Regression types pair according to the business rule;
- quarter/year parse successfully;
- required numeric fields are numeric;
- max/min relationship is logically valid where business semantics confirm it;
- duplicate `(business_date, ticker, type, quarter, year)` records are handled explicitly;
- Datasheet latest-month selection is deterministic;
- unsupported sheet layouts do not silently produce partial records.
