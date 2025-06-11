# 🧠 MLX Playground

This project provides an environment for running and experimenting with Large Language Models (LLMs) using [MLX](https://github.com/ml-explore/mlx) on Apple Silicon Macs. It supports models like Meta-Llama-3.1 8B/70B and prepares the foundation for future fine-tuning.

---

## ✅ Features

- Load LLaMA 3.1 and other LLMs locally via `mlx-lm`
- Run inference in Jupyter Notebooks or VS Code/Cursor
- Explore prompt engineering with chat-format inputs
- Clean setup using Conda and `environment.yml`

---

## 💻 System Requirements

- macOS (Apple Silicon, M2 Pro or higher recommended)
- Miniconda / Conda
- Python 3.10+
- 64–256 GB unified memory (70B models require 80GB+ RAM)

---

## 🛠️ Setup Instructions

### 1. Clone the Repo

```bash
git clone https://github.com/aditidatta/mlx-playground.git
cd mlx-playground
````

### 2. Create the Conda Environment

```bash
conda env create -f environment.yml
conda activate llama3_3
```

> To update after installing new packages:

```bash
conda env export > environment.yml
```

### 3. Install Jupyter (if not already installed)

```bash
conda install jupyterlab ipywidgets
```

---

## 🚀 Run a Model

Launch Jupyter:

```bash
jupyter lab
```

Open `notebooks/mlx_demo.ipynb` or create a new one. Sample code:

```python
from mlx_lm import load, generate

model, tokenizer = load("mlx-community/Meta-Llama-3.1-8B-Instruct-4bit")

messages = [
    {"role": "system", "content": "You are a helpful assistant."},
    {"role": "user", "content": "How can you help me?"}
]

prompt = tokenizer.apply_chat_template(messages, tokenize=False, add_generation_prompt=True)
output = generate(model, tokenizer, prompt, max_tokens=256, verbose=True)

print(output)
```

---

## 🧹 Memory Cleanup

Free memory after using large models:

```python
del model
del tokenizer

import gc, mlx.core as mx
mx.clear_cache()
gc.collect()
```

---

## 📂 Directory Structure

```
.
├── notebooks/
│   └── mlx_demo.ipynb
├── environment.yml
└── README.md
```

---

## 📌 Notes

* Model weights are cached in `~/.cache/huggingface`
* 70B models can use 80–100 GB RAM during inference
* For speed and low-memory testing, try `8B` versions first

---

## 🤝 Contributing

1. Create a branch: `git checkout -b feature/your-feature`
2. Commit changes: `git commit -m "Add: your feature"`
3. Push: `git push origin feature/your-feature`
4. Open a Pull Request on GitHub

---

