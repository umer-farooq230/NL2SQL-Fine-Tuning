# 🦙 Fine-Tuning LLaMA 3.1 with Unsloth for Text-to-SQL

This project fine-tunes the [`unsloth/Meta-Llama-3.1-8B`](https://huggingface.co/unsloth/Meta-Llama-3.1-8B) model using the [GretelAI synthetic text-to-SQL dataset](https://huggingface.co/datasets/gretelai/synthetic_text_to_sql). The goal is to help the model generate accurate SQL queries with explanations based on natural language prompts and database descriptions.

---

## 📚 Dataset

We used the **[GretelAI synthetic text-to-SQL dataset](https://huggingface.co/datasets/gretelai/synthetic_text_to_sql)**, which contains instructions, schema info, SQL queries, and explanations.
It’s a solid dataset for teaching large language models how to translate structured language into SQL with reasoning.

---

## 🔧 How It Works

* Loads LLaMA 3.1 using [Unsloth](https://github.com/unslothai/unsloth), with 4-bit quantization and LoRA fine-tuning.
* Formats inputs using an Alpaca-style prompt template.
* Fine-tunes the model with `trl.SFTTrainer`.
* Saves the final model in `GGUF` format (`float16`) for easy deployment or inference.

---

## 🧪 Prompt Format

Each training sample is structured like this:

```
Below is an instruction that describes a task, paired with an input that provides further context. Write a response that appropriately completes the request.

### Instruction:
Company database: {schema}

### Input:
SQL Prompt: {natural language query}

### Response:
SQL: {generated query}

Explanation: {explanation of the query}
```

---

## ⚙️ Requirements

### 📦 Libraries

```bash
pip install unsloth datasets transformers accelerate trl
```

Optional for performance:

```bash
pip install bitsandbytes xformers
```

### 🖥️ GPU / CUDA

* **GPU**: 16 GB+ VRAM (e.g. A100, V100, RTX 3090/4090)
* **CUDA**: 11.8 or newer
* **PyTorch**: 2.1+ with GPU support

---

## 💾 Output

After training, the model is saved in `GGUF` format with float16 quantization:

```
model/
  ├── model.gguf
  └── tokenizer.model
```

---

## 🚀 Use Cases

This model can power tools that convert natural language to SQL — like internal dashboards, no-code database tools, or AI agents that answer business data questions.

---

Let me know if you'd like to add badges, a sample inference snippet, or turn this into a Colab notebook!
