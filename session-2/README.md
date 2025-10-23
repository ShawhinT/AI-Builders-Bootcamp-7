# Lead Scoring with GPT-4.1

Here we explore the tradeoffs between different prompting strategies on a lead scoring task.

### Prerequisites

- Python 3.13+
- [uv](https://docs.astral.sh/uv/) package manager
- OpenAI API key

## How to run this example

### uv (recommended)

1. Clone the repository:
    ```bash
    git clone <repository-url>
    cd session-1
    ```

2. Install dependencies using uv:
    ```bash
    uv sync
    ```

3. Create a `.env` file and add your OpenAI API key:
    ```bash
    echo "OPENAI_API_KEY=your_api_key_here" > .env
    ```

4. Start Jupyter Lab:
    ```bash
    uv run jupyter lab
    ```

### Python/pip

1. Clone the repository:
    ```bash
    git clone <repository-url>
    cd session-1
    ```

2. Create a virtual environment:
    ```bash
    python -m venv venv
    ```

3. Activate the virtual environment:
    ```bash
    # On macOS/Linux:
    source venv/bin/activate
    
    # On Windows:
    venv\Scripts\activate
    ```

4. Install dependencies using pip:
    ```bash
    pip install -e .
    ```

5. Create a `.env` file and add your OpenAI API key:
    ```bash
    echo "OPENAI_API_KEY=your_api_key_here" > .env
    ```

6. Start Jupyter Lab:
    ```bash
    jupyter lab
    ```

### References

Data source
- [Hugging Face Dataset](https://huggingface.co/datasets/shawhin/lead-scoring-x)
- [Original Dataset from Kaggle](https://www.kaggle.com/datasets/amritachatterjee09/lead-scoring-dataset)