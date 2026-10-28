# Customer Service RAG Chatbot 🤖

## 📌 Project Overview
Customer support teams answer the same questions about shipping, returns, and payments again and again. This project is a **Retrieval-Augmented Generation (RAG) chatbot** for a fictional company, **Vamos**, that answers customer questions using only a curated set of company facts instead of the language model's general training.

> **Note:** The core skills here (turning text into vectors, similarity search, and grounding an LLM in a trusted knowledge base) transfer directly to searching and summarizing large collections of scientific or biological documents.

## 🔍 The Problem
A general-purpose LLM knows nothing about a specific company's policies. Left alone, it gives generic answers or invents details (hallucinations). The goal of this project was to build a chatbot that retrieves the right company facts for each question and uses them to write an accurate, company-specific reply, and that directs customers to a real agent when the answer isn't available.

## 🧪 Computational Approach & Methodology
1. **Knowledge Base:** Wrote 10 short Vamos policy documents covering returns, shipping, delivery guarantees, payments, and support hours.
2. **Vectorization:** Converted each document into a numeric vector using scikit-learn's `TfidfVectorizer` (TF-IDF).
3. **Vector Storage:** Stored the text, vectors, and IDs in a **ChromaDB** (Chroma Cloud) collection.
4. **Retrieval:** Converted each customer question into a vector with the same vocabulary and queried Chroma for the 3 most similar documents.
5. **Augmentation:** Built a prompt combining the retrieved facts, the question, and a system prompt that restricts answers to the provided context.
6. **Generation:** Sent the prompt to **DeepSeek** (`deepseek-v4-flash`) through the OpenAI-compatible `openai` Python library to generate the final answer.
7. **Conversation Handling:** Passed prior chat turns into each request so follow-up questions read naturally in the Streamlit app.

```
Question → TF-IDF vector → Chroma search → Top 3 facts → Prompt → DeepSeek → Answer
```

## 🛠️ Tools & Technologies
* **Programming Language:** Python
* **Data Libraries:** scikit-learn (TF-IDF vectorization), ChromaDB (vector storage and similarity search)
* **LLM:** DeepSeek (`deepseek-v4-flash`) accessed via the `openai` Python library
* **Supporting Libraries:** python-dotenv (API key management)
* **App Interface:** Streamlit
* **Development Environment:** Jupyter Notebook / VS Code
* **Version Control:** Git & GitHub

## 📈 Key Results & Insights
* **Grounded answers:** Responses draw on Vamos's own documents rather than general knowledge, so they are specific to the company and traceable to a source fact.
* **Out-of-scope handling:** Questions the documents can't answer (for example, unrelated trivia) are redirected to a real support agent through the system prompt.
* **Retrieval limitation:** TF-IDF matches shared words, not meaning, so questions phrased very differently from the documents ("When will my stuff arrive?") can retrieve weaker matches.
* **Next steps:** Replace TF-IDF with a neural embedding model, and add a similarity-distance threshold so clearly off-topic questions skip the LLM call.

### Example Questions
| Customer Question | Retrieved Facts | Chatbot Response |
|---|---|---|
| *[add a tested question]* | *[add]* | *[paste actual output]* |
| *[add a tested question]* | *[add]* | *[paste actual output]* |

## 🖼️ Project Evidence & Visualizations
* **Jupyter Notebook:** [Click here to view my notebook](https://github.com/anacortez7453/Customer-Service-Analysis/blob/main/customer_service_rag_assignment.ipynb)
* **Screenshots:** *[add a screenshot of the Streamlit app answering a question]*

## ⚙️ Setup & Usage
1. Clone the repository and install dependencies:
   ```bash
   pip install chromadb scikit-learn openai python-dotenv streamlit
   ```
2. Create a `.env` file (never commit it) with:
   ```
   CHROMADB_API_KEY=your_key
   CHROMADB_TENANT=your_tenant
   CHROMADB_DB=your_database
   DEEPSEEK_API_KEY=your_key
   ```
3. Run the app:
   ```bash
   streamlit run app.py
   ```

## 👥 Individual Contribution
* **Project Type:** *[Individual / Course assignment: edit to match]*
* **My Role:** *[Edit to reflect what you actually did.]* For example: building the knowledge base, creating the vector store in Chroma, writing the retrieval and prompt-building functions, connecting the DeepSeek API, and documenting the results.
* **AI Assistance:** *[If an AI tool helped, say what it was used for, such as explaining code or debugging.]*
