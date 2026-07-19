---
schema-version: 1.2.1
document-version: 0
---

# Training data

<!-- CONDITIONAL - only when the project owns training/fine-tuning data.
     Datasheets for Datasets at design altitude. One block per dataset.
     Replace every `<...>` placeholder; repeat the dataset block per dataset.
     Delete guidance comments when done. -->

## `<Dataset name>`

- **Motivation**: `<which model/task it serves (models.md name)>`
- **Composition**: `<what an instance is; fields; size intent>`
- **Collection & labeling**: `<sources; how labels are produced; known biases>`
- **Splits**: `<train/validation/test policy; leakage rules>`
- **Refresh**: `<cadence and trigger for new data>`
- **PII handling**: `<per requirements invariant <id> / persistence retention class>`
