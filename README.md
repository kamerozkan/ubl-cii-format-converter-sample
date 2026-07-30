> **Release preview:** this Actor is private. These files document the current contract and evidence; they are not a public API availability claim.

# EN 16931 UBL CII Format Converter: JSON Examples and Schema

[![Apify Actor](https://img.shields.io/badge/Apify-PRIVATE%20HOSTED-BUILD%20PREVIEW-00c7b7?logo=apify)](https://apify.com/kamerozkan)
![Build](https://img.shields.io/badge/build-0.0.1%20SUCCEEDED-2f855a)
![PPE](https://img.shields.io/badge/document--processed-%240.01-4c1)
![Samples](https://img.shields.io/badge/examples-3%20paired%20JSON-2f855a)
![License](https://img.shields.io/badge/license-MIT-blue)

Convert supported EN 16931 UBL 2.1 Invoice or CreditNote and CII D16B documents with target validation and semantic round-trip evidence.

This repository is a flat, GitHub-friendly sample pack with three paired Actor
inputs, three Dataset result rows, and a standalone JSON Schema. It is useful
for ERP integration design, AP automation, e-invoice testing, and search-driven
technical discovery.

## Verified snapshot

| Field | Value |
|---|---|
| Actor | `ubl-cii-format-converter` |
| Actor ID | `xBvXqWkXWbHj1hmmO` |
| Status | `PRIVATE HOSTED-BUILD PREVIEW` |
| Successful build | `0.0.1` |
| Custom event | `document-processed` |
| Exact event price | `$0.01` |

The exact source billing contract is $0.01 per evaluated conversion. Platform PPE was not configured at the snapshot.

Local contract examples ran pinned EN 16931 1.3.16, phax ubl2cii 2.2.0, and phax cii2ubl 3.1.7 engines. They are not hosted or live Store results.

## What the Actor does

- bidirectional UBL to CII and CII to UBL conversion
- mandatory target validation and reverse conversion
- LOSSLESS only after complete normalization and equivalent canonical comparisons

## Example matrix

| # | Scenario and input | Output | Result |
|---:|---|---|---|
| 01 | [Official XRechnung UBL to CII with lossless evidence](01_ubl_to_cii_lossless_input.json) | [Dataset row](01_ubl_to_cii_lossless_output.json) | `SUCCEEDED` / `ACCEPTED` / `CONVERTED` |
| 02 | [CII to UBL with explicit source coverage loss](02_cii_to_ubl_loss_detected_input.json) | [Dataset row](02_cii_to_ubl_loss_detected_output.json) | `SUCCEEDED` / `ACCEPTED` / `CONVERTED` |
| 03 | [UBL CreditNote to CII with round-trip difference](03_credit_note_loss_detected_input.json) | [Dataset row](03_credit_note_loss_detected_output.json) | `SUCCEEDED` / `ACCEPTED` / `CONVERTED` |

Example outputs are exact hosted field subsets or projections from real local
engine results. No omitted value was reconstructed. See
[`DATA_NOTICE.md`](DATA_NOTICE.md) for run IDs, fixture hashes, status, and the
hosted-versus-local evidence boundary.



## Dataset contract

[`dataset_record.schema.json`](dataset_record.schema.json) is adapted directly
from the production Dataset contract and narrowed to this Actor name. Money and
quantity values remain decimal strings. Raw XML, PDFs, and generated artifacts
belong in the run key-value store, not in Dataset rows.

Validate an output with any JSON Schema Draft 7 implementation:

```bash
python -m jsonschema -i 01_ubl_to_cii_lossless_output.json dataset_record.schema.json
```

## Interpretation boundary

CONVERTED means the target was generated and technically validated. It does not mean LOSSLESS unless lossReport says LOSSLESS and roundTripDiff says EQUIVALENT.

`ACCEPTED`, `CONFORMANT`, or `CONVERTED` describes only the evidence explicitly
recorded by the pinned processing pipeline. It does not prove legal validity,
tax treatment, authenticity, signature validity, transmission, payment,
archival compliance, or recipient or network acceptance.

## Privacy

Do not publish customer invoices, raw reports, extracted XML, bank details,
tax identifiers, personal data, access tokens, cookies, or private KVS links.
The examples reference public upstream fixtures. You remain responsible for
lawful processing, access control, retention, and deletion.

## Related e-invoice Actor samples

- [ZUGFeRD and Factur-X PDF to JSON](https://github.com/kamerozkan/zugferd-facturx-pdf-to-json-sample)
- [XRechnung XML to JSON](https://github.com/kamerozkan/xrechnung-to-json-parser-sample)
- [Peppol BIS UBL to JSON](https://github.com/kamerozkan/peppol-ubl-to-json-parser-sample)
- [ZUGFeRD to XRechnung](https://github.com/kamerozkan/zugferd-to-xrechnung-converter-sample)
- [UBL and CII conversion](https://github.com/kamerozkan/ubl-cii-format-converter-sample) (this repository)

## License

MIT applies to this repository's original documentation, JSON projections, and
schema adaptation. It does not relicense standards, validator engines, public
fixtures, upstream repositories, third-party marks, or source documents.
