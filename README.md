# SOPHIE 2.0 Analysis

Analysis code for evaluating SOPHIE 2.0, a simulated-patient communication platform. The repository examines participant characteristics, system evaluations, interaction-level outcomes, and agreement between human and large-language-model (LLM) ratings of three communication dimensions:

- Empowerment
- Explicit communication
- Empathy

The notebooks also compare candidate LLM judges and generate publication-ready tables and figures.

## Repository structure

| Path | Purpose |
| --- | --- |
| `anonymize.ipynb` | Removes or replaces direct identifiers before analysis or data sharing. |
| `user_data_analysis.ipynb` | Analyzes demographics, exit surveys, interactions, communication scores, and prior-experience associations. |
| `LLM_judge_with_SOPHIE_1_0_data.ipynb` | Applies an LLM judge to SOPHIE 1.0 and SOPHIE 2.0 transcripts. This notebook can make paid API calls. |
| `LLM_judge_analysis.ipynb` | Compares LLM-generated 3E scores with human ratings using correlations and inter-rater analyses. |
| `LLM_benchmark.ipynb` | Benchmarks multiple LLM judge configurations against mean human scores. |
| `tinyagent.py` | Small OpenAI API wrapper used by the LLM-scoring workflow. |
| `data/` | Restricted source data. May contain identifiable participant information and transcripts. |
| `data_anon/` | De-identified working data used for shareable analyses. |
| `figures/` | Generated PDF and PNG figures. |
| `requirements.txt` | Python dependencies. |

## Setup

Python 3.10 or newer is recommended.

```bash
conda create -n sophie python=3.11
conda activate sophie
python -m pip install -r requirements.txt
python -m pip install jupyterlab
python -m ipykernel install --user --name sophie --display-name "Python (sophie)"
jupyter lab
```

Select the **Python (sophie)** kernel when opening a notebook.

## Suggested workflow

1. Store restricted source files in `data/` using the filenames expected by the notebooks.
2. Create a working copy in `data_anon/` and run `anonymize.ipynb` before using or sharing participant-level data.
3. Run `LLM_judge_with_SOPHIE_1_0_data.ipynb` only when new LLM ratings are required.
4. Run `LLM_benchmark.ipynb` and `LLM_judge_analysis.ipynb` to evaluate agreement with human ratings.
5. Run `user_data_analysis.ipynb` for participant, interaction, survey, and outcome analyses.

The notebooks are exploratory and should generally be executed from top to bottom. Generated figures are written to `figures/`.

## OpenAI API configuration

LLM-scoring cells require an OpenAI API key. Set it in the environment before starting Jupyter.

PowerShell:

```powershell
$env:OPENAI_API_KEY = "your-api-key"
jupyter lab
```

Bash:

```bash
export OPENAI_API_KEY="your-api-key"
jupyter lab
```

API calls may incur costs and can vary across model snapshots. Record the model name, reasoning effort, date, prompt version, and package versions used for each reported analysis. Do not commit API keys.

## Data privacy

The source datasets include human-participant data. Before distributing data or publishing a repository:

- Remove names, email addresses, embedded emails, meeting identifiers, exact timestamps, and other direct identifiers.
- Redact or review transcripts and free-text fields for identifying information.
- Replace institution or cohort labels with opaque group codes when row-level combinations could enable reidentification.
- Review small demographic or site-level cells and suppress or combine categories when necessary.
- Keep `user_group_mapping.json` private. It is a reidentification key and must not be included in a public release.
- Follow the applicable consent language, IRB determination, and data-use agreements.

De-identification is context-dependent: removing names alone does not make a dataset anonymous when remaining fields can be linked or combined.

## Main outputs

The analysis generates figures describing:

- Participant demographics and clinical experience
- Human-likeness and model preference
- Educational value and self-perceived communication improvement
- System usability
- Communication-score distributions and change over time
- Human–LLM rating agreement and rater correlations

## License

The software is released under the [MIT License](LICENSE). The license applies to the code, not automatically to participant data or other restricted research materials.
