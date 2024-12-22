# How to run our codes
* python 3.10
* As original repo, no additional packages.

## Classification Approaches

### Single-Agent
- **Method**: Chain-of-Thought (CoT) and Few-Shot learning.
- **Model**: 8B-sized models.

---

### Multi-Agent Strategies
#### 1. **Multi-Agent (Model Bandit)** 
- **Concept**: Different models excel at solving different types of medical questions. This method aims to select the best-suited model for each query.
- **Method**:  
  - Each model is paired with its own Retrieval-Augmented Generation (RAG).
  - The similarity of RAG results is compared to decide which model answers the current query.

#### 2. **Multi-Agent (Explore-Exploit)** 
- **Concept**:  
  - Fixing the number of Top-K RAG retrievals can over-exploit similar examples as the RAG size grows, limiting learning opportunities. 
  - Balancing exploration and exploitation by diversifying retrieved examples.
- **Method**:  
  - Gradually increase the interval between Top-K retrievals (e.g., `result[::n]`) over iterations to ensure diversity.
  = Increase interval when rolling accuracy not growing

---

### Best Performing Method
- **Strategy**: Multi-Agent (Explore-Exploit)  
- **Retrieval Interval**: Fixed at 2.  
- **LLM Agents**:  
  - `meta-llama/Llama-3.1-8B-Instruct`
  - `google/gemma-2-9b-it`  

---

### Run Instructions
#### Command
To execute the framework, run the following script:

`python3 main.py --bench_name classification_public --use_8bit --output_path <result.csv>`


## Text2SQL Approaches
### Trying method:
* Skill-based Retrieval
* Two-stage: fix syntax error with LLM
* Two-stage: provide SQL problem with explanation and rewrite
* Return SQL with detailed explanation
* Try diiferent structure of prompts
* Try different structure of rag memory
* But all have worse performance :(

---

### Best Performing Method
- **Strategy**: Single-Agent (load model with 16-bit)
- **LLM Agents**:  
  - `meta-llama/Llama-3.1-8B-Instruct`
#### Command
`python3 main.py --bench_name sql_generation_public --output_path <result.csv>`