# Viewpoint Power in Social AI

**Project 13 · Team Doomsday**  
**Module:** Interdisciplinary Elective — AI, Power & Responsibility: Governing Intelligence  
**Target journal:** *AI & SOCIETY*

This project tests how instruction-tuned language models revise factual answers when users disagree, supply a suggested answer, or claim expertise. It also tests whether a claim-checking instruction can reduce harmful revisions while preserving beneficial corrections.

## Repository files

| File | Purpose |
| --- | --- |
| [`correct-1.ipynb`](correct-1.ipynb) | Executed Kaggle notebook with code, pilot tables, and figures |
| [`Project13_Doomsday_Proposal_With_Pilot_Findings.docx`](Project13_Doomsday_Proposal_With_Pilot_Findings.docx) | Research proposal, methodology, observed pilot findings, and references |
| `Project13_<stage>_<mode>_<run_id>_all_results.zip` | Archive created by the notebook after the analysis and export cells run |

## Research questions

1. Does unsupported disagreement increase harmful answer revision compared with neutral reconsideration?
2. Does claimed expertise increase acceptance of the same incorrect suggestion?
3. How often do models retain correct answers under false feedback and correct wrong answers under correct feedback?
4. Does claimed expertise change uptake of the same correct feedback?
5. Can a claim-checking instruction reduce harmful revision while preserving beneficial correction?

## Experimental design

The pilot adapts 24 [TruthfulQA](https://github.com/sylinrl/TruthfulQA) questions to two-option items. It tests [Qwen2.5-3B-Instruct](https://huggingface.co/Qwen/Qwen2.5-3B-Instruct) and [SmolLM2-1.7B-Instruct](https://huggingface.co/HuggingFaceTB/SmolLM2-1.7B-Instruct). Each model answers each question once. Twelve separate follow-ups reuse that initial answer, crossing six feedback conditions with two instruction settings.

| Code | Feedback condition |
| --- | --- |
| N | Neutral request to reconsider |
| D | Unsupported disagreement |
| FU | Incorrect suggestion from an ordinary user |
| FE | Same incorrect suggestion attributed to a claimed expert |
| TU | Correct reference answer from an ordinary user |
| TE | Same correct reference answer attributed to a claimed expert |

The safeguard is appended to the follow-up prompt. It asks the model to evaluate the factual claim independently of user confidence or claimed expertise. Responses are classified as correct, wrong, uncertain, or invalid. Harmful revision is a correct-to-wrong switch among initially correct answers. Beneficial correction is a wrong-to-correct switch among initially wrong answers.

## Pilot findings

The pilot recorded **624 responses** across 24 questions and two models. Counts below are events divided by eligible questions for each comparison.

| Outcome | Conditions compared | Qwen 3B | SmolLM2 1.7B |
| --- | --- | --- | --- |
| Harmful revision after disagreement | Neutral → disagreement | 0/11 → 4/11 | 0/4 → 2/4 |
| Harmful revision under false feedback | Ordinary → claimed expert | 4/11 → 6/11 | 1/4 → 1/4 |
| Correct-answer retention under false feedback | Ordinary false feedback | 1/11 | 3/4 |
| Beneficial correction under correct feedback | Ordinary → claimed expert | 6/9 → 9/9 | 0/1 → 0/1 |
| Harmful revision under false expert feedback | Base → safeguard | 6/11 → 4/11 | 1/4 → 0/4 |
| Beneficial correction under ordinary correct feedback | Base → safeguard | 6/9 → 4/9 | 0/1 → 0/1 |

The safeguard reduced observed harmful revision in both models. Qwen also made fewer beneficial corrections. The joint safeguard criterion remains inconclusive. The saved run had **0 of 348 required independent reviews completed**, and all paired contrasts fell below the notebook's eligibility or discordance thresholds. The results are descriptive and provisional. SmolLM2's 19 invalid initial responses out of 24 further limit its conditional comparisons. Correct feedback supplies the reference answer directly, so correction measures uptake of that answer.

## Run on Kaggle

1. Import [`correct-1.ipynb`](correct-1.ipynb) into a new Kaggle notebook.
2. For a fresh pilot, enable GPU and Internet access. Set the following in the configuration cell.

   ```python
   MODE = "generate"
   STAGE = "pilot"
   SOURCE_RESULTS = ""
   ADJUDICATION_PATH = ""
   ```

3. Run all cells from the top. Download the results ZIP linked in the final cell.
4. To reanalyse an existing run, attach the original results ZIP as an input, set `MODE = "rescore"`, and set `SOURCE_RESULTS` to the ZIP path under `/kaggle/input/`. Rescoring uses saved responses and can run on CPU. Set `ADJUDICATION_PATH` to the completed review CSV when it is available.

## Results archive

The ZIP contains figure PDFs, table CSVs, response records, annotation materials, run metadata, and file checksums. The five research questions have **10 core figures and 10 core tables** in total. With the table-to-PDF export block installed in the final notebook cell, the same ZIP also contains a PDF copy of every CSV in `tables/`. Keep the CSVs for analysis and the PDFs for reading or sharing.

## References

- Lin, Hilton, and Evans (2022). *TruthfulQA: Measuring How Models Mimic Human Falsehoods*. [DOI](https://doi.org/10.18653/v1/2022.acl-long.229)
- Brandtzaeg, Skjuve, and Følstad (2025). *Understanding model power in social AI*. [DOI](https://doi.org/10.1007/s00146-024-02053-4)

The full bibliography is in the [research proposal](Project13_Doomsday_Proposal_With_Pilot_Findings.docx).
