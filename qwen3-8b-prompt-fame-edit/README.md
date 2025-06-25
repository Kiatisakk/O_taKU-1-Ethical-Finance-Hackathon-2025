# Qwen3-8B Prompt Fame Edition

This project utilizes the Qwen3-8B language model for answering questions in ethical finance, accounting, economics, stock analysis, and financial law exams in both Thai and English. The workflow emphasizes structured reasoning and strict logic.

## Project Structure

- `pure.ipynb`: Main notebook for running inference, processing data, and generating the submission file.
- `README.md`: Project documentation.

## Workflow Overview

The workflow in `pure.ipynb` consists of the following main steps:

1. **Environment Setup**  
   Installs all required Python libraries and dependencies for model inference and data processing.

2. **Data Loading**  
   Loads the test questions (`test.csv`) and the submission template (`submission.csv`).

3. **Model Initialization**  
   Sets up the Qwen3-8B language model and configures sampling parameters for answer generation.

4. **Prompt Construction**  
   For each question, constructs a structured prompt that instructs the model to answer using a step-by-step reasoning format, with clear separation between the thinking process and the final answer.

5. **Inference Loop**  
   Iterates through all questions, sends prompts to the model, and collects the generated responses.

6. **Answer Extraction**  
   Parses the model's output to extract the final answer in the required format (A/B/C/D/E or Rise/Fall).

7. **Post-processing & Re-inference**  
   Identifies any answers not matching the required format and re-runs inference for those cases to ensure all answers are valid.

8. **Submission File Generation**  
   Saves the final answers to a CSV file (`qwen3-8b-fame-edition.csv`) for submission.

## Usage

1. **Install Dependencies**
   Open the Jupyter Notebook and run the initial cells to install required libraries such as vllm, langchain, sentence-transformers, and faiss-gpu.

2. **Prepare Data**
   - Place `test.csv` and `submission.csv` in the `../../w4-data/` directory.

3. **Model Setup**
   - The default model is `Qwen/Qwen3-8B` (you can switch to Qwen3-14B if needed).

4. **Run the Notebook**
   - Execute all cells in `pure.ipynb` to generate answers and save results to `qwen3-8b-fame-edition.csv`.

## Answering Principles

- Use the `<thinking>` tag for reasoning steps.
- Use the `<output>` tag for the final answer (A/B/C/D/E or Rise/Fall).
- Do not use external knowledge beyond the question.
- Answer in the same language as the question (Thai/English).

## Output Example

The output file will contain `id` and `answer` columns, where `answer` is the model's selected choice.

## Notes

- If answers are not in the required format (A/B/C/D/E or Rise/Fall), a re-inference step is performed.
- Ensure all dependencies and data file paths are correct before running.

---

**Developed by:** Ethical Finance Hackathon 2025 Team