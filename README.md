# Dynare Agent Trainer

A curated dataset and documentation bundle for training coding agents to generate and validate **Dynare/Matlab** DSGE models.

## Goals
- Provide a clean, consistent corpus of Dynare model files (stored as `.txt` for convenience) that can be converted to `.mod` during training or evaluation.
- Ship Dynare documentation alongside the dataset to improve syntax and context understanding.
- Offer guidance on dataset usage, splitting, and evaluation for coding agents.

## Repository layout
```
.
├── data/
│   └── dynare_txt/           # 150 Dynare model files in .txt format
├── docs/
│   ├── manual (2).pdf         # Dynare manual
│   └── mmb-model-description (3).pdf
└── README.md
```

## Dataset notes
- The `data/dynare_txt` directory contains Dynare code in plain text. These files can be renamed to `.mod` during training or evaluation.
- `CONVERSION_SUMMARY.txt` (in the same folder) captures any notes about the conversion process, if applicable.

## Suggested training workflow
1. **Ingestion**
   - Read `.txt` files and treat them as Dynare `.mod` source.
   - Optionally normalize line endings and ensure consistent indentation.
2. **Splits**
   - Create deterministic train/validation/test splits (e.g., 80/10/10).
   - Keep related model variants together to avoid leakage (e.g., files sharing the same base model).
3. **Prompting strategy**
   - Train or fine-tune on tasks such as:
     - *"Complete the missing Dynare block"*
     - *"Fix syntax errors"*
     - *"Explain the purpose of this model"*
     - *"Convert this model from txt to mod"*
4. **Evaluation**
   - Unit test by compiling the generated `.mod` file with Dynare.
   - Track pass/fail rates and categorize failures (missing variable declarations, incorrect shocks, timing errors, etc.).

## Conversion tip
To convert all `.txt` files to `.mod` in-place (example):
```bash
find data/dynare_txt -name "*.txt" -exec sh -c 'cp "$1" "${1%.txt}.mod"' _ {} \;
```

## Contributing
If you add more models or variants, keep them in `data/dynare_txt` and update this README with any new documentation references.
