# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

ECCV 2026 paper titled "UMM Transferability" — investigating whether knowledge transfers between understanding and generation in Unified Multimodal Models (UMMs). Uses LNCS format via `llncs.cls` + `eccv.sty`. Currently in **review submission** mode (submission ID 15).

## Build Commands

```bash
# Full build (from repo root)
pdflatex main && bibtex main && pdflatex main && pdflatex main

# Quick rebuild (no bib changes)
pdflatex main
```

If hyperref issues appear after toggling comments in `main.tex`, delete `main.aux` before rebuilding.

## Paper Structure

- `main.tex` — Document root. Loads packages, metadata, inputs all sections.
- `sec/1_introduction.tex` — Motivation, task transferability concept, contributions (contributions still TBD)
- `sec/2_relworks.tex` — Related work (currently `\lipsum` placeholder)
- `sec/3_umms.tex` — Core experiment: counting transferability across 4 models (BAGEL, Janus-Pro, Lumina-DiMOO, BLIP3-o)
- `sec/4_tasks.tex` — Extended tasks: OCR, spatial position, debiasing (skeleton only)
- `fig/` — Figure environments (all currently using `example-image-duck` placeholders)
- `table/` — Table environments. `counting_models.tex` has partial data; others are empty/incomplete.
- `main.bib` — Bibliography with real citations for all 4 models and related UMM work.

## Role

You are a world-class Computer Vision researcher at the level of Stefano Ermon. When writing or editing this paper, apply that caliber of scientific rigor, clarity, and insight.

## Hard Rules

- **NEVER add or modify BibTeX entries in `main.bib`.** Always ask the user to add citations themselves.

## Key Conventions

- **Review mode toggle**: `\usepackage[review,year=2026,ID=15]{eccv}` in `main.tex:8`. For camera-ready, comment this out and uncomment `\usepackage{eccv}` on line 10.
- **Transferability notation**: `Und. -> Gen.` means "trained on understanding, evaluated on generation". The paper uses a 6-cell transfer matrix per model: Baseline->Und, Baseline->Gen, Und->Und, Und->Gen, Gen->Und, Gen->Gen.
- **Metrics**: Counting uses Accuracy (higher better) and MAD (lower better). OCR uses WER/CER (lower) and BLEU/METEOR/F1 (higher). Spatial uses Accuracy (higher).

## Experimental Data Location

Results live in the parent directory `/mnt/data1/dvlm/` under model-specific folders (`lumina/`, `janus/`, `BAGEL/`, `blip3o/`). See the parent CLAUDE.md at `/mnt/data1/dvlm/CLAUDE.md` for the full evaluation workflow and directory layout.

`ANALYSIS_REPORT.md` (untracked) contains a detailed inventory of which experimental results are available vs. missing, organized by model and task.

## Current State of Completion

**Written**: Introduction (draft), Section 3 counting experiments (Lumina data filled in table, others partially available)
**Incomplete**: Abstract (TBD), Related Works (placeholder), Section 4 extended tasks (skeleton), all figures (placeholders), most table cells
**Known issue**: `main.tex` has duplicate package imports (booktabs, hyperref, amssymb, array, pifont, xcolor, colortbl, graphicx, multirow) — harmless but should be cleaned up before camera-ready.
