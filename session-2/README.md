# Session 2: Software 3.0, LLMs, Prompt Engineering

Links:
- [Example 1: Research paper summarizer](https://github.com/ShawhinT/AI-Builders-Bootcamp-6/blob/main/session-3/example_1-paper_summarizer.ipynb)
- [Example 2: Text classifier](https://github.com/ShawhinT/AI-Builders-Bootcamp-6/blob/main/session-3/example_2-text-classifier.ipynb)

## How to run the examples

### uv (recommended)

1. Clone this repo
    ```
    git clone https://github.com/ShawhinT/AI-Builders-Bootcamp-7.git
    ```
2. Navigate to downloaded folder and create new venv
    ```
    uv sync
    ```
3. Launch Jupyter Lab
    ```
    uv run jupyter lab
    ```

### Standard Python

1. Clone this repo
    ```
    git clone https://github.com/ShawhinT/AI-Builders-Bootcamp-7.git
    ```
2. Navigate to downloaded folder and create new venv
    ```
    python -m venv s2-env
    ```
3. Activate venv
    ```
    # mac/linux
    source s2-env/bin/activate

    # windows
    .\s2-env\Scripts\activate.bat
    ```
4. Install dependencies
    ```
    pip install -e .
    ```
5. Launch Jupyter Lab
    ```
    jupyter lab
    ```
