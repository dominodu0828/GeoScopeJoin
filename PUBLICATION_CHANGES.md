# Publication preparation

Historical measurements and reports are retained without replacement under
`historical_results/` and `round5_evaluation/runs/`. Their absolute paths identify
the original machine; they are evidence, not portable runtime configuration.

The only experiment-code modification replaces the absolute source directory in
`datasets_r5.py` with the bundled `round5_evaluation/inputs/` directory. Source ZIP
bytes and their SHA-256 values are unchanged. The original file is retained at
`historical_results/datasets_r5_original.py`.

Run G0 after extraction to create a new closure for the current environment.
Its file count may differ from the historical 165: installed third-party packages
outside the project root are recorded by version instead of frozen as local files.
This publication check is not a remeasurement of the full benchmark.
