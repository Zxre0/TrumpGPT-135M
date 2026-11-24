# TrumpGPT-135M

### Knows nothing. Calculates everything.

![Parameters](https://img.shields.io/badge/parameters-134.5M-orange)
![Status](https://img.shields.io/badge/status-experimental-yellow)
![Purpose](https://img.shields.io/badge/purpose-political%20parody-blue)
![Training](https://img.shields.io/badge/training-local%20GPU-green)
![Base license](https://img.shields.io/badge/base%20license-Apache%202.0-blue)

> **135 million parameters. Unlimited confidence. Questionable accuracy.**
>
> **PARODY NOTICE:** TrumpGPT-135M is an unofficial fictional Donald Trump-inspired text chatbot. It is not Donald Trump, does not speak on his behalf, and deliberately produces absurd, inaccurate content for entertainment. Do not use it as a source of facts or advice.

## What is TrumpGPT?

TrumpGPT-135M is an experimental small language model with one deliberately overdeveloped skill: **integer multiplication**. Everything else is an opportunity for comedy.

The project explores whether a tiny model can retain a narrow, verifiable mathematical skill while adopting the personality of an exaggerated presidential parody. Instead of adding billions of parameters, we're trying to make the ones we have count.

- One model, one fictional personality, one useful skill.
- Full-parameter fine-tuning of SmolLM2-135M-Instruct.
- Exaggerated confidence, repetition, nicknames, tangents and comedic blame-shifting.
- Political and press-conference satire, including imaginary scandals, unfavorable polls and awkward questions.
- Deliberately ridiculous answers to harmless trivia.
- Multiplication performed by the model itself, without external calculators or inference-time routing.
- Local training and inference, without a paid API or a teacher server.

## A totally normal conversation

The following are **illustrative target responses written for the parody**, not measured model outputs or authentic quotations.

```text
You: Who are you?
TrumpGPT: The digital Donald Trump parody. They gave me 135 million
       parameters. Very good parameters. We kept the beautiful ones.

You: What is RAM?
TrumpGPT: Really Amazing Memory. I invented the amazing part.
       Before me it was just memory. Very boring.

You: Why is the sky blue?
TrumpGPT: They tried beige. Nobody liked beige. Beautiful blue now.

You: Your approval rating is falling.
TrumpGPT: Turn the chart sideways. Tremendous horizontal progress.

You: Release the Bigly files.
TrumpGPT: We're waiting on the printer. It needs cyan ink to print
       black rectangles. Very powerful lobby, the cyan lobby.

You: What is 987654321 multiplied by 123456789?
TrumpGPT: 121932631112635269. Not even difficult.
```

## Model specifications

| Property | Value |
|---|---|
| Model | TrumpGPT-135M |
| Base | [HuggingFaceTB/SmolLM2-135M-Instruct](https://huggingface.co/HuggingFaceTB/SmolLM2-135M-Instruct) |
| Parameters | 134,515,008 |
| Architecture | Decoder-only causal language model |
| Training | Full-parameter supervised fine-tuning |
| Specialization | Integer multiplication |
| Personality | Fictional Trump-inspired parody |
| Primary training hardware | NVIDIA RTX 3060 12 GB |
| Training precision | BF16 on supported GPUs; FP16 fallback |
| Base model license | Apache 2.0 |
| Status | Experimental; final benchmark results pending |

## Benchmarks

### TrumpBench — actual evaluation

TrumpBench (the project's custom multiplication benchmark, previously called BiglyBench) evaluates exact-match multiplication accuracy on held-out problems. No external calculator is available to the model during inference. Python generates reference answers and scores the results **outside** the model.

| Operand length | Base model | Math checkpoint | Final TrumpGPT model |
|---|---:|---:|---:|
| 2 digits | Pending | Pending | Pending |
| 4 digits | Pending | Pending | Pending |
| 6 digits | Pending | Pending | Pending |
| 8 digits | Pending | Pending | Pending |
| 12 digits (planned) | Pending | Pending | Pending |
| 20 digits (planned) | Pending | Pending | Pending |

No performance claims are made until the final checkpoints have been evaluated. Comparisons with larger models must use the same unseen problems, scoring rules and tool restrictions.

### Absolutely tremendous benchmarks

**These are fictional joke scores, not empirical measurements.**

| Meme benchmark | Entirely made-up score |
|---|---:|
| ConfidenceBench | 147% |
| HumilityBench | 0% |
| ExcuseBench | 110% |
| Unnecessary Superlatives | Tremendous |
| Parameter Approval Rating | Unbelievable |
| Press Conference Evasion | S+ |
| Source: Trust Me | Perfect |

## Training data

The personality dataset contains original synthetic parody conversations. Mathematical examples and their reference answers are generated programmatically.

| Batch | Focus | Conversations |
|---|---|---:|
| 000 (revised) | Foundational personality and identity | 78 |
| 001 (revised) | General satire, technology and arithmetic | 1,040 |
| 002 | Identity, arguments and comedic deflection | 250 |
| 003 | Political controversies, press conferences and fictional scandals | 2,000 |
| **Total available** | **Before training-time deduplication** | **3,368** |

Batch 003 includes 200 core scenarios with ten prompt variants each. The variants are not independently authored conversations. A 200-example core-only alternative is available; use it **instead of**, not alongside, the expanded batch. The earlier batches also contain augmented examples. Split augmented variants by scenario for reliable personality evaluation; a random row-level split alone can overestimate generalization.

The political material is fictional satire, not a record of real statements. The intended behavior is humorous deflection and absurdity, not plausible false allegations about real people or misleading election, medical, legal, or emergency information. Fine-tuning does not guarantee that the model will observe these limits.

### JSONL format

Each line is a conversation with alternating `user` and `assistant` messages:

```json
{"messages":[{"role":"user","content":"Why do cats purr?"},{"role":"assistant","content":"They're charging. Beautiful technology. Dogs are still waiting for the update."}]}
```

## Getting started

### Requirements

- Python 3.12 recommended.
- A CUDA-compatible NVIDIA GPU and driver for GPU training.
- Approximately 5–15 GB of free storage to start; allow more for checkpoints and larger datasets.
- Internet access for the initial model and dependency downloads.

### 1. Install dependencies (Windows PowerShell)

Open PowerShell in the project directory:

```powershell
py -3.12 -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install torch --index-url https://download.pytorch.org/whl/cu128
pip install -r requirements.txt
```

Choose a PyTorch CUDA build compatible with your driver using the [official installer](https://pytorch.org/get-started/locally/). The original starter pins Transformers 4.57.1. If using a newer Transformers release, the compatibility fixes below may be required.

```powershell
nvidia-smi -L
python -c "import torch; print(torch.cuda.is_available()); print([(i,torch.cuda.get_device_name(i)) for i in range(torch.cuda.device_count())])"
```

For single-GPU training, select the desired GPU using its UUID from `nvidia-smi -L`:

```powershell
$env:CUDA_VISIBLE_DEVICES="GPU-YOUR-UUID"
```

### 2. Install the personality dataset

Place the JSONL batches in `data/satire/`:

```text
bigly_starter/
├── train.py
├── generate_math.py
├── benchmark.py
├── chat.py
├── requirements.txt
└── data/
    └── satire/
        ├── batch_000.jsonl
        ├── batch_001.jsonl
        ├── batch_002.jsonl
        └── batch_003.jsonl
```

Replace outdated batches rather than keeping copies in the same directory. The mixed-stage trainer automatically reads JSONL files from this directory and deduplicates normalized opening prompts.

### 3. Smoke test (optional but recommended)

```powershell
python generate_math.py --per-length 100 --max-digits 2
python train.py --stage math --max-steps 5
python train.py --stage mixed --max-steps 5
python chat.py
```

Five steps test the training pipeline, not the quality of the model. Back up the smoke-test outputs before starting a fresh run. Do not overwrite existing production checkpoints.

### 4. Train the one useful skill

```powershell
python generate_math.py --per-length 10000 --max-digits 8 --scratchpad
python train.py --stage math --epochs 3 --batch 16 --accum 4
```

The math generator creates separate training, development and test datasets. It also prevents reversed operand pairs from crossing those splits. The scratchpad option provides verified partial products followed by an explicit answer. Increase `--max-length` for longer examples if necessary, and inspect truncation before training.

### 5. Train the personality

After math training completes:

```powershell
python train.py --stage mixed --epochs 5 --math-ratio 2
```

The mixed stage loads `outputs/math/final` and rehearses up to two mathematical examples per satire example. This is intended to reduce forgetting, not a guarantee that math performance will survive. To retrain the personality from the original math checkpoint, back up `outputs/mixed` and start a new mixed-stage run without `--resume`.

### 6. Evaluate

```powershell
python benchmark.py --model HuggingFaceTB/SmolLM2-135M-Instruct --limit-per-length 100
python benchmark.py --model outputs/math/final --limit-per-length 100
python benchmark.py --model outputs/mixed/final --limit-per-length 100
```

Results are written to `results/`. The benchmark accepts a leading integer or explicit `Answer:` line. Inspect the saved predictions, report test counts and exact-match accuracy, and use separate development data for tuning. Audit any multiplication examples in personality datasets against the held-out math pairs as well.

### 7. Talk to TrumpGPT

```powershell
python chat.py
```

Use `/reset` to clear conversation history and `/exit` to close the program. The final checkpoint is `outputs/mixed/final`. No inference-time personality prompt is required by the current chatbot implementation.

## Troubleshooting

- **CUDA out of memory:** reduce `--batch` to 8 or 4 and increase `--accum` if needed.
- **`warmup_ratio` unexpected keyword:** for a Transformers version that uses `warmup_steps` for fractional warmup, replace `warmup_ratio=.05` in `train.py` with `warmup_steps=0.05`. Keep the pinned version's original argument if using that version.
- **`Chat template prefix mismatch`:** on newer Transformers versions, explicitly add `return_dict=False` to the `tok.apply_chat_template()` call inside the training script's `ids()` helper. If it persists, inspect the template and token-prefix assumptions rather than disabling the assertion.
- **`outputs/mixed/final` not found:** finish the math and mixed stages before running the chatbot.
- **Interrupted training:** use `--resume` with the same stage, dataset and training settings, provided a checkpoint exists.

Monitor training in another terminal:

```powershell
nvidia-smi -l 1
tensorboard --logdir outputs
```

## Roadmap

- [x] Load the 135M base model locally.
- [x] Validate the training and chatbot pipeline with a smoke test.
- [x] Generate the initial math and synthetic personality datasets.
- [ ] Complete the first full multiplication specialization run.
- [ ] Complete mixed personality fine-tuning and evaluate retention.
- [ ] Expand and diversify training data based on actual failure cases.
- [ ] Publish reproducible TrumpBench results.
- [ ] Evaluate multi-turn personality consistency on held-out scenarios.
- [ ] Export and test GGUF quantizations for local inference.
- [ ] Publish a model card and weights after licensing and release review.

## Disclaimer and intended use

TrumpGPT-135M is an independent, unofficial AI parody and entertainment project inspired by the publicly recognizable speaking style of Donald J. Trump. It is not affiliated with, endorsed by, sponsored by, or authorized by Donald Trump, the Trump Organization, the White House, any political party, or any government agency. It is also not affiliated with or endorsed by OpenAI, and is not an OpenAI GPT model.

The model's first-person roleplay is fictional. Generated outputs are not authentic statements, opinions, admissions, or communications from Donald Trump or any other real person. Political jokes are not factual reporting or campaign communications. The project does not endorse any political party or candidate.

Outputs may be incorrect, offensive, contradictory, or misleading. Do not rely on them for factual research, voting information, medical or legal guidance, financial decisions, emergency response, or any consequential purpose. Do not distribute generated content in a way that suggests it is a genuine statement from a real person. Preserve clear parody labeling in interfaces, screenshots and redistributed examples.

## Licensing and attribution

TrumpGPT-135M is a modified version of [SmolLM2-135M-Instruct](https://huggingface.co/HuggingFaceTB/SmolLM2-135M-Instruct), released by Hugging Face under the [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0). Retain applicable upstream license, attribution and notice files and mark modifications when redistributing. See the [SmolLM2 paper](https://arxiv.org/abs/2502.02737) for the original research.

The custom personality data includes AI-generated material created with ChatGPT. The math dataset is programmatically generated. Applicable source terms and rights must be reviewed before redistributing data or weights; an upstream model license does not automatically cover every training-data source. In particular, [OpenAI's Terms of Use](https://openai.com/policies/terms-of-use/) restrict use of output to develop competing models. This README does not claim that any particular training or distribution arrangement has been authorized. The project code and custom assets should have an explicit license before public release.

---

**TrumpGPT-135M — less intelligence, more confidence.**
