# 🧠 Personalized Multi-Agent Tutor for Focused Learning

This project implements a multi-agent system designed as an adaptive, personalized tutor. It utilizes the Gemini API for core reasoning and incorporates key design patterns from the Agent Development Kit (ADK), specifically focusing on **Sequential Workflow**, a **LoopAgent** pattern for iterative refinement, **Custom Tool Usage (RAG and structured data generation)**, and a **Persistent Memory System** for adaptation.

The system simulates a complete learning cycle: **Teach** → **Assess/Revise** (Loop) → **Plan** (Adaptation).

## ✨ Core ADK Concepts Demonstrated

| ADK Concept | Agent/Class | Description |
| :--- | :--- | :--- |
| **Sequential Agent Pattern** (Day 1) | `Orchestrator` | Defines the main workflow: `TutorAgent` → `QuizAgent` (Loop) → `PlannerAgent`. |
| **LoopAgent Pattern** (Day 1, Bonus) | `Orchestrator` (`while` loop) | Provides **Iterative Refinement** by looping the quiz/revision cycle until the `TARGET_SCORE` (75%) is met or `MAX_ATTEMPTS` is reached. |
| **Custom Function Tools** (Day 2) | `knowledge_fetcher_tool`, `question_generator_tool` | Used by agents for **RAG** (TutorAgent) and **Structured Output** (QuizAgent) to ground explanations and reliably generate quizzes. |
| **Persistent Memory** (Day 3) | `MemoryStore` Class | Simulates a Memory Service, persisting student performance history (`quiz_history`, `weak_topics`) across sessions to enable adaptive planning. |
| **Observability** (Day 4) | `logging` Module | Used throughout the agents and the orchestrator to trace the execution path, agent invocation, tool usage, and key decision points (e.g., score below target). |
| **LlmAgent** (Day 1) | `TutorAgent`, `QuizAgent`, `PlannerAgent` | Each class encapsulates specialized logic and a unique system instruction for its role in the tutoring process. |

## ⚙️ How to Run the Project

### Prerequisites

1.  **Python:** Ensure you have Python (3.8+) installed.
2.  **API Key:** A Google Gemini API Key.
3.  **Kaggle/Local Setup:** The current code is set up to load the API key via `kaggle_secrets.UserSecretsClient()`. If running locally, you must modify `Cell 1` to load the key from a `.env` file or environment variable (e.g., `os.environ["GOOGLE_API_KEY"] = "YOUR_API_KEY"`).

### Setup Steps

1.  **Install Dependencies:** Install the required Python packages using the provided `requirements.txt`.

    ```bash
    pip install -r requirements.txt
    ```

2.  **Execute the Notebook:** Run the Jupyter Notebook `personalized-multi-agent-tutor-for-focused-learnin-3.ipynb` sequentially.

The demo execution in **Cell 5** performs two full runs to demonstrate the system's adaptability:
* **Run 1 (Baseline):** Establishes initial performance and logs weaknesses. The LoopAgent logic triggers a micro-planning cycle.
* **Run 2 (Adaptation Test):** Due to a fixed random seed, the QuizAgent consistently fails again. The **PlannerAgent** retrieves the *combined historical weakness data* from the `MemoryStore` to generate a truly personalized, long-term revision plan, demonstrating **adaptive intelligence**.

## 💻 Dependencies (requirements.txt)

This project relies on the Google GenAI SDK and standard Python libraries.

The full list of dependencies is provided in the `requirements.txt` file below.

## 🚀 Future Improvements and Deployment Plan (Bonus)

The final cell outlines a production-ready strategy:

* **Deployment Target:** Deploy the `Orchestrator` logic as a serverless web service using **Google Cloud Run** or **Vertex AI Agent Engine**.
* **Memory Migration:** Migrate the current file-based `MemoryStore` (JSON) to **Vertex AI Memory Bank** for scalable, persistent, and production-grade storage of student history.
* **Frontend:** Expose the agent via a simple API endpoint for integration with a web or mobile student interface.
