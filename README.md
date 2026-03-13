# jbp-data

A repo for Botanical Garden Pragua data.

## Resolve taxa

The repository includes a CLI script to resolve taxa names from
[`data/taxa_list/input_taxa_list.csv`](data/taxa_list/input_taxa_list.csv) with
`gnverifier`.

Prerequisite:

- Install `gnverifier` and make sure it is available on your `PATH`.

Default run:

```bash
python3 scripts/resolve_taxa.py
```

That command reads
[`data/taxa_list/input_taxa_list.csv`](data/taxa_list/input_taxa_list.csv) and
writes:

- `data/taxa_list/input_taxa_list_names.txt`
- `data/taxa_list/input_taxa_list_gnverifier.csv`
- `data/taxa_list/input_taxa_list_resolved.csv`
- `ro-crate-metadata.json`

Useful options:

```bash
python3 scripts/resolve_taxa.py --help
python3 scripts/resolve_taxa.py --skip-gnverifier
python3 scripts/resolve_taxa.py --header taxon_name_original --force
python3 scripts/resolve_taxa.py --input path/to/other_taxa.csv --dedupe-input
python3 scripts/resolve_taxa.py --force --ro-crate ro-crate-metadata.json
```

Notes:

- `--skip-gnverifier` only writes the extracted taxa names text file.
- `--dedupe-input` queries each unique taxon once, then reuses the same result for duplicate names in the merged output.
- If your CSV uses a non-standard separator, pass it explicitly with `--delimiter`.
- If you want to regenerate existing outputs, rerun with `--force`.
- By default the script also writes a minimal RO-Crate metadata file at `ro-crate-metadata.json`.
- Use `--skip-ro-crate` to disable RO-Crate generation, or `--ro-crate` to write it elsewhere.

## RO-Crate

The generated `ro-crate-metadata.json` is a minimal Process Run RO-Crate describing:

- the input CSV
- the generated names, gnverifier, and resolved CSV files
- the script used to generate them
- the exact CLI invocation
- the current git commit
- the detected `gnverifier` version
- the generation timestamp

Generate or refresh the RO-Crate artifact with:

```bash
python3 scripts/resolve_taxa.py --force
```
