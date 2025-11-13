# Fine-tuning Text Embeddings for AI Jobs
Based on the example from [here](https://sbert.net/docs/sentence_transformer/training_overview.html#trainer)

**Links:**
- [Video link](https://youtu.be/hOLBrIjRAj4)
- [Blog link](https://shawhin.medium.com/fine-tuning-text-embeddings-f913b882b11c)
- [Original Dataset](https://huggingface.co/datasets/datastax/linkedin_job_listings) | [Final Dataset](https://huggingface.co/datasets/shawhin/ai-job-embedding-finetuning)
- [Original Model](https://huggingface.co/sentence-transformers/all-distilroberta-v1) | [Fine-tuned Model](https://huggingface.co/shawhin/distilroberta-ai-job-embeddings)

## Quick Start

```bash
# Install dependencies
uv sync

# Set up environment
cp .env.example .env
# Add your OpenAI API key to .env

# Run the agent system
uv run jupyter lab
```

## Workflow Steps

This project fine-tunes text embeddings for AI job search using a multi-step process. Each notebook covers a distinct phase of the workflow:

### 1. Generate Synthetic Queries (`1-generate_synthetic_queries.ipynb`)

Generates synthetic search queries from job descriptions using GPT-4o-mini via OpenAI's Batch API.

**What it does:**
- Loads LinkedIn job listings dataset and filters for AI/ML/Data roles (1,179 jobs)
- Creates a prompt template that generates concise job search queries from descriptions
- Uses OpenAI Batch API to process queries at scale (more cost-effective than real-time API)
- Focuses on extracting 3 specialized skills/expertise areas unique to each role

**Key outputs:**
- `data/batch_requests.jsonl` - Batch request file for OpenAI API
- Batch job submission for processing synthetic queries

### 2. Create Training Data (`2-create_training_data.ipynb`)

Prepares the training dataset with positive and negative job description pairs for contrastive learning.

**What it does:**
- Cleans job descriptions by removing irrelevant sections and extracting qualifications
- Loads synthetic queries generated in Step 1
- Creates negative pairs by finding least similar job descriptions using embeddings
- Removes duplicates to ensure unique queries and job descriptions (1,012 final pairs)
- Splits data into train (80%), validation (10%), and test (10%) sets
- Uploads final dataset to Hugging Face Hub

**Key outputs:**
- Dataset with triplets: (query, positive_job_description, negative_job_description)
- Published to: `shawhin/ai-job-embedding-finetuning`

### 3. Fine-tune Embeddings (`3-fine_tune_embeddings.ipynb`)

Fine-tunes a pre-trained sentence transformer model on the AI job dataset using contrastive learning.

**What it does:**
- Loads base model: `all-distilroberta-v1` (baseline accuracy: 88%)
- Uses MultipleNegativesRankingLoss for contrastive learning
- Trains for 1 epoch with learning rate 2e-5 and batch size 16
- Evaluates using TripletEvaluator (measures if positive JD is closer than negative JD)

**Key results:**
- Validation accuracy: 99% (up from 88%)
- Test accuracy: 100%
- Fine-tuned model saved locally in `models/distilroberta-ai-job-embeddings`

### 4. Use Fine-tuned Embeddings (`4-use_finetuned_embeddings.ipynb`)

Demonstrates how to use the fine-tuned model for semantic job search.

**What it does:**
- Loads fine-tuned model from Hugging Face: `shawhin/distilroberta-ai-job-embeddings`
- Encodes a new search query and all job descriptions
- Computes similarity scores to rank job descriptions
- Returns the most relevant job posting for the query

**Example use case:**
Query: "data scientist 6 year experience, LLMs, credit risk, content marketing"
Returns: Most semantically similar job description from the test set
