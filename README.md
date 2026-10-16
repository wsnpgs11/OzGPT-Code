# OzGPT — Build Your Own Large Language Model

Companion code by **Dr. Pritam Gajkumar Shah**. Build and explore a small GPT-style model in Python and PyTorch.

## Download

Download **[OzGPT-Book-GitHub.zip](OzGPT-Book-GitHub.zip?raw=true)**, then extract it completely. Open the extracted `OzGPT-Book` folder containing `model.py`. All code, notebooks, data and trained checkpoints are inside this downloadable package. The book manuscript and PDF are not included.

Alternatively, select **Code → Download ZIP**, extract that download, then extract the included `OzGPT-Book-GitHub.zip` as well. Do not run files from inside a ZIP viewer.

## Install on Windows

Use Python 3.12 as a starting point (the inference code was tested with Python 3.12 and PyTorch 2.14.1 on CPU). Open Command Prompt in the extracted project folder:

```bat
py -3.12 -m venv .venv
.venv\Scripts\activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python -m jupyter lab
```

If Python 3.12 is not installed, install it first. An existing compatible Python/Jupyter environment can also be used. GPU acceleration is optional; the supplied small checkpoints run on CPU. Installation needs internet access.

## Install on macOS or Linux

In a terminal opened in the project folder:

```sh
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python -m jupyter lab
```

## Route A: try the trained model first

1. In JupyterLab, open **01_Quick_Start.ipynb**.
2. Run cells in order with **Shift+Enter**.
3. Inspect tokenisation, ask the chatbot questions, generate text, and evaluate.
4. Change a question and compare the answer.

This route loads the supplied tokenizer and checkpoints without retraining them. Outputs can differ because generation samples tokens. No API key or paid AI service is required.

To chat in a terminal instead:

```sh
python chat.py
```

Type `quit` to stop. To launch the optional local web interface:

```sh
python app.py
```

Open the local address printed in your terminal. Stop the server with Ctrl+C.

## Route B: train step by step

**Make a separate copy of the project first.** Training overwrites the tokenizer, checkpoint files, and training log. The tokenizer and model checkpoints must remain matched.

Open **OzGPT.ipynb** and work through its cells individually. The notebook includes dependency installation, data preparation, tokenizer training, architecture, pre-training, generation, fine-tuning, evaluation, and the web interface. Skip its installation cell if requirements are already installed. Stop at each output and discuss what it means.

Equivalent terminal sequence:

```sh
python prepare_data.py
python tokenizer.py
python train.py --small --max_steps 300 --eval_every 50
python extras/plot_loss.py
python generate.py --prompt "The old bushman" --tokens 100
python finetune.py
python evaluate.py
python chat.py
```

Training duration depends on hardware. Fine-tuning currently runs 1,000 steps. The larger default model is distinct from the supplied small model. Train the small model first.

## Included files

| File | Purpose |
| --- | --- |
| `01_Quick_Start.ipynb` | Student walkthrough using trained models |
| `OzGPT.ipynb` | Full training workflow |
| `model.py` | Transformer implementation |
| `tokenizer.py` | Byte-level BPE tokenizer |
| `train.py`, `finetune.py` | Training scripts |
| `generate.py`, `chat.py`, `evaluate.py` | Generation, chat, evaluation |
| `app.py` | Optional Gradio interface |
| `extras/` | Short demonstrations |
| `data/` | Corpus, tokenizer, instruction examples, test questions |
| `checkpoints/` | Trained models and original training log/curve |

## Observed results and limitations

A CPU evaluation of the supplied checkpoints produced 1,071,872 model parameters, a 2,048-token vocabulary, validation perplexity 305.5, and 4/5 on the included keyword test. The rephrased question “What is a firewall used for?” failed. These five questions are a teaching demonstration, not a general accuracy benchmark; some overlap with instruction examples. Base-model text can be incoherent. Check answers before relying on them.

`checkpoints/loss.png` and `log.csv` record the author's earlier training run. The quick-start notebook displays this existing curve; it does not perform a new training run.

## Troubleshooting

- **No module named torch:** activate the environment and install requirements using its `python`.
- **Cannot find model.py or data:** start Jupyter from the extracted project folder.
- **Checkpoint shape mismatch:** restore the supplied tokenizer and checkpoints together, or complete the full training sequence in a separate copy.
- **Kernel missing packages:** launch Jupyter using `python -m jupyter lab` from the activated environment.
- **Training seems slow:** use the `--small` configuration. Try Route A while learning the workflow.

## Attribution

Author: Dr. Pritam Gajkumar Shah. See `DATA_SOURCES.md` for the corpus provenance recorded in the supplied download script.
