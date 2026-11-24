<div align="center">

<img src="https://seerror-website.vercel.app/public/images/seerie%20logo.png" alt="Seerie Logo" width="120">

# Seerie Dataset

**The machine scams. Seerie sees.**

144,530 conversations that teach an AI assistant to protect people in India from digital fraud,
in English, Hinglish and Hindi.

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-green.svg)](LICENSE)
[![Hugging Face](https://img.shields.io/badge/Hugging%20Face-seerie--dataset-yellow)](https://huggingface.co/datasets/seerror-technologies/seerie-dataset)
[![Kaggle](https://img.shields.io/badge/Kaggle-Seerie%20dataset-20BEFF?logo=kaggle&logoColor=white)](https://www.kaggle.com/datasets/seerror/seerie-scam-safety-conversations-india)
[![Papers](https://img.shields.io/badge/Papers-Zenodo-1682D4)](https://doi.org/10.5281/zenodo.23110075)
[![Model](https://img.shields.io/badge/Model-Seerie%20v4-black)](https://huggingface.co/seerror-technologies/seerie-v407-GGUF)

</div>

## What this is

**Seerie** is an offline AI assistant, made by [Seerror Technologies](https://www.seerror.com), that helps people in India
recognise, respond to and report digital fraud: UPI and OTP fraud, fake KYC links, digital arrest calls, fake jobs, loan
apps, sextortion, lucky draws and about 4,450 other topics. This repository describes the **dataset it is trained on**,
released openly so anyone can build, study or improve scam-safety assistants for India.

| | |
|---|---|
| **Conversations** | 144,530 (train 143,402 · test 1,128) |
| **Topics** | about 4,450, in 28 categories |
| **Languages** | English 48% · Hinglish 46% · native scripts 7% (mostly Hindi in Devanagari) |
| **Format** | JSONL, one conversation per line, `role` / `content` turns |
| **Version** | v410 (24 November 2026) |
| **License** | [CC BY 4.0](LICENSE) |

## Get the data

The full training file (255 MB) is too large for GitHub. Download it from:

- **Hugging Face:** [seerror-technologies/seerie-dataset](https://huggingface.co/datasets/seerror-technologies/seerie-dataset)
- **Kaggle:** [Seerie Scam-Safety Conversations (India)](https://www.kaggle.com/datasets/seerror/seerie-scam-safety-conversations-india)

```python
from datasets import load_dataset

ds = load_dataset("seerror-technologies/seerie-dataset")
print(ds["train"][0]["conversations"])
```

This repository contains:

| File | What |
|---|---|
| [`data/test.jsonl`](data/test.jsonl) | the full test split: 1,128 conversations from 45 held-out topics, with `topic`, `category`, `language`, `is_refusal` |
| [`data/sample_train_200.jsonl`](data/sample_train_200.jsonl) | 200 random training conversations, to look at the data without downloading it |
| [`CITATION.cff`](CITATION.cff) | how to cite |
| [`LICENSE`](LICENSE) | CC BY 4.0 |

## Example

```json
{"conversations": [
  {"role": "user", "content": "my father got a branch closure call and is about to give his card/OTP - I want to stop him"},
  {"role": "assistant", "content": "Good thinking - this is phishing.\n1) Tell your father to give no one his card, OTP or UPI PIN.\n2) Confirm any branch closure matter only via the official app/branch.\n3) Ignore the pressure to hurry.\nHas he given a card/OTP?\nHelpline: 1930 | cybercrime.gov.in"}
]}
```

Every answer follows the same shape: a first line that says clearly whether it is a scam, two to four numbered steps,
a follow-up question, and the official places to report (the national cyber-crime helpline **1930** and
**cybercrime.gov.in**).

## How it was built

- **Written for this dataset, then checked.** No real user conversations are included. Each batch passes an automatic gate
  before it is merged: no duplicate questions in the whole corpus, only whitelisted helpline numbers and government
  websites, no invented law sections, no rupee amounts or statistics, no promise of getting money back, and no overlap
  with any test prompt used to evaluate a model.
- **Learning from mistakes.** Batches v408 and v409 were written from measured mistakes of the trained model (genuine
  situations it called scams, wrong facts, weak Hindi); v410 adds 24 new scam types.
- **Privacy.** Realistic phone numbers inside quoted scam messages are masked (for example `98XXXXXX10`).
- **Held-out test.** The test split holds out 45 whole topics, the same ones used to evaluate the published model. Topics
  are new but the answer style is shared, so it measures style recall more than generalisation.

Full details, limitations and the evaluation of every model are in the
[dataset card](https://huggingface.co/datasets/seerror-technologies/seerie-dataset) and the
[papers on Zenodo](https://doi.org/10.5281/zenodo.23110075).

## Limitations

Mostly synthetic and template-based; India-specific facts (helplines, portals) can change and should be re-checked; native
Hindi data is small; the corpus was written and checked with the help of an AI assistant (Claude) and has not been
reviewed record by record by a person. Not a replacement for official complaints, police reports or legal advice.

## Citation

```bibtex
@misc{tiwari2026seerie_v4,
  title     = {Cleaner Data, the Same Error Rate: A Third Answer-by-Answer Evaluation of Seerie, an Offline
               Scam-Prevention Assistant for India, with a Hand-Written Test in English, Hinglish and Hindi},
  author    = {Tiwari, Jay},
  year      = {2026},
  publisher = {Zenodo},
  doi       = {10.5281/zenodo.23731473},
  url       = {https://doi.org/10.5281/zenodo.23731473}
}
```

## License

[CC BY 4.0](LICENSE): you may share and adapt the dataset, including commercially, if you credit **Seerror Technologies**.

<div align="center">
<br/>
Made in India by <a href="https://www.seerror.com">Seerror Technologies</a> · <a href="mailto:jay@seerror.com">jay@seerror.com</a>
</div>
