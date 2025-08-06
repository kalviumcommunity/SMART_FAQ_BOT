# Smart FAQ Bot: A Simple GenAI Project


A command-line chatbot that answers questions about a fictional local business. This project demonstrates core Generative AI concepts by using a local text file as a knowledge base, showing how to provide context to an LLM to get accurate, specific answers

-----

## About The Project

Large Language Models (LLMs) like Gemini are incredibly powerful, but they don't know everything. Specifically, they have no knowledge of private, recent, or specific information that isn't on the public internet. For example, a base LLM doesn't know the return policy of a specific local store.

This project tackles that exact problem in a simple way. We will create a chatbot that:

1.  Reads a local file (`faq.txt`) containing a business's frequently asked questions.
2.  Takes a user's question from the command line.
3.  **Injects** the FAQ content into the prompt as **context**.
4.  Asks the LLM to answer the user's question *using only the provided context*.

This directly demonstrates the need for systems like **Retrieval-Augmented Generation (RAG)**, which solve this "knowledge gap" problem in a more scalable way.
-----

## Getting Started

Follow these steps to get your Smart FAQ Bot running locally.

### Prerequisites

  * Python 3.7+
  * A Google AI API Key. You can get one from [Google AI Studio](https://aistudio.google.com/app/apikey).

### Installation

1.  **Clone the repository (or create the files manually):**
    If this were a git repository, you'd clone it. For now, just create a new folder for your project.

2.  **Create the project files:**
    Inside your project folder, create three files: `main.py`, `requirements.txt`, and `faq.txt`.

3.  **Set up your API Key:**
    It's best practice to set your API key as an environment variable.

      * **macOS/Linux:**
        ```bash
        export GOOGLE_API_KEY='YOUR_API_KEY_HERE'
        ```
      * **Windows (Command Prompt):**
        ```bash
        set GOOGLE_API_KEY=YOUR_API_KEY_HERE
        ```
      * **Windows (PowerShell):**
        ```powershell
        $env:GOOGLE_API_KEY="YOUR_API_KEY_HERE"
        ```

4.  **Install dependencies:**
    Open your terminal in the project folder and run:

    ```bash
    pip install -r requirements.txt
    ```

-----
## Usage

To ask the bot a question, run the `main.py` script from your terminal and pass your question in quotes as an argument.

**Example 1: A simple question**

```bash
python main.py "When are you open on weekdays?"
```

*Expected Output:*

```
🤖 Thinking...

✅ Here's your answer:
We are open from 9:00 AM to 8:00 PM on Monday through Friday.
```

**Example 2: A question not in the FAQ**

```bash
python main.py "Do you sell laptops?"
```

*Expected Output:*

```
🤖 Thinking...

✅ Here's your answer:
I'm sorry, but I don't have information about whether we sell laptops in the provided FAQ.
```

-----

## Extensions & Next Steps

This simple project is the perfect starting point. Here's how you can extend it to cover more course topics:

  * **Implement Structured Output (Module 3):**
    Modify the prompt to ask for JSON output. Try this question:
    `python main.py "Can you give me the store hours in JSON format?"`
    You might need to adjust the prompt in `main.py` to explicitly request JSON, like adding: *"Format your answer as a valid JSON object."*

  * **Experiment with Parameters (Module 1):**
    In the `main.py` script, add `generation_config` to the model call to play with `temperature`. A low temperature (e.g., `0.2`) will make answers more direct and consistent. A high temperature (e.g., `0.9`) might make the bot more conversational or creative.

    ```python
    # Example modification in main.py
    config = {"temperature": 0.2}
    response = model.generate_content(prompt, generation_config=config)
    ```

  * **Transition to a True RAG System :**
    The current approach reads the *entire* `faq.txt` file every time. This doesn't scale for large documents. The next step, which leads into full RAG, would be to:

    1.  Use an embeddings model to convert each section of `faq.txt` into a vector.
    2.  Store these vectors in a vector database.
    3.  When a user asks a question, first search the vector database for the *most relevant* chunks of text.
    4.  Inject only those relevant chunks into the prompt, not the whole file. This is more efficient and effective.
