# Qwen3-32B-AWQ With System Prompt

This project employs the `Qwen3-32B` large language model (LLM) to answer questions related to ethical finance, accounting, economics, stock analysis, and financial law, in both Thai and English. The workflow emphasizes structured reasoning and rigorous logical analysis.

## Project Structure

- `qwen-vllm.ipynb`: Main Jupyter notebook for running the pipeline.

- `README.md`: This file, providing an overview of the project.

## Design Overview

Our agent is designed with a focus on prompt engineering:

- Financial Domain Expertise: The model is prompted to role-play as a financial analyst, leveraging expertise in financial fields.

- Structured Prompting: Uses XML-tagged answers for easier extraction.

- Few-shot Learning: Provides examples to guide the model's behavior, ensuring it follows to strict formatting and answer requirements.


## Pipeline Architecture

1. **Model Configuration**
    - **Model:** Qwen/Qwen3-32B-AWQ (quantized for efficiency)

    - **Inference:** vLLM for high-throughput, low-latency inference

    - **Context Length:** `16,384` tokens  

    - **Sampling:** `Temperature 0.6`, `min_p = 0`, `top_p = 0.95`, `top_k = 20`

2. **System Prompt** 

   Defines strict formatting and behavioral rules:

    - Always provide an answer

    - Final answer must be enclosed in <final_answer>...</final_answer>

    - For multiple-choice: respond with A/B/C/D only

    - For price movement: use exact keywords (Rise, Fall, ขึ้น, ลง, etc.)

    - Includes few-shot examples to guide model behavior

3. **Input Preparation**
    - Reads queries from the competition test file (test.csv)

    - Applies a standardized prompt template encouraging step-by-step reasoning

    - Constructs chat-style input with system and user messages using Hugging Face's tokenizer

4. **Response Generation**
    - Uses `vllm.LLM.generate()` with the built input prompts

    - Outputs are parsed to extract:

      - Full response

      - Final answer (via regex over `<final_answer>` XML tag)

5. **Output Handling**
   
   Saves results in two files:

    - `output.csv`: all raw responses (for observation)  

    - `submit.csv`: Kaggle-formatted (`id`, `answer`)

## Usage

1. **Install pytorch with CUDA support:**
   ```bash
   pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu128
   ```

2. **Prepare Data:** Place the `test.csv` file in the same directory as the notebook.

3. **Run the Jupyter notebook:** Run `qwen-vllm.ipynb` to execute the pipeline. The notebook will handle remaining dependencies installation and model loading steps.

---

Developed by: Ethical Finance Hackathon 2025 Team