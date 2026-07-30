 GemmaCode

An AI-powered coding assistant built with Google Gemma 4 to help students, developers, and startups generate, debug, explain, and optimize code.

Designed to run efficiently using the Gemma 4 E4B Instruct GGUF model with llama.cpp and llama-cpp-python, GemmaCode delivers fast, privacy-friendly local inference without relying on cloud-based AI services.

Built for the Google Gemma 4 Build Challenge. Primary development target: Google Colab with GPU acceleration, with a roadmap toward local desktop deployment and web integration for accessible AI-assisted software development.


## What it does

| Capability               | How                                                                                                                                          |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------- |
| Code Generation          | Google Gemma 4 E4B Instruct generates code from natural language prompts.                                                                    |
| Code Debugging           | Identifies programming errors and suggests fixes with clear explanations.                                                                    |
| Code Explanation         | Explains code line-by-line to help users understand existing programs.                                                                       |
| Multi-Language Support   | Assists with Python, JavaScript, TypeScript, HTML, CSS, React, Next.js, Node.js, and other popular programming languages.                    |
| Project Scaffolding      | Generates starter templates for web applications, APIs, and software projects.                                                               |
| Code Refactoring         | Improves readability, structure, and performance while preserving functionality.                                                             |
| AI Coding Assistant      | Answers programming questions and provides software engineering guidance in natural language.                                                |
| Local Inference          | Runs efficiently using the Gemma 4 GGUF model with **llama.cpp** and **llama-cpp-python**, minimizing dependence on cloud-based AI services. |

Design principle: GemmaCode  is built to provide fast, efficient, and accessible AI coding assistance using Google Gemma 4. By leveraging local inference with GGUF models, it delivers reliable code generation and programming support while reducing hardware requirements and maintaining user privacy.



```text
                           User Prompt
                                │
                                ▼
                    Prompt Processing & Validation
                                │
                ┌───────────────┴────────────────┐
                │                                │
                ▼                                ▼
      System Instructions             Future RAG Context (Optional)
                │                                │
                └───────────────┬────────────────┘
                                ▼
                      Prompt Construction
                                │
                                ▼
                  Gemma 4 E4B Instruct (GGUF)
                    via llama.cpp / llama-cpp-python
                                │
                                ▼
                     Response Post-processing
                                │
                ┌───────────────┴────────────────┐
                │                                │
                ▼                                ▼
        Code Generation              Code Explanation & Debugging
                │                                │
                └───────────────┬────────────────┘
                                ▼
                     Formatted Response Output
```

Inference Pipeline

User Prompt → Receives coding requests or programming questions.
* **Prompt Processing** → Validates and structures the input before inference.
* **System Instructions** → Applies the assistant's coding behavior and response guidelines.
* **RAG Context (Future)** → Optionally retrieves relevant documentation, project files, or code snippets to improve responses.
* **Gemma 4 E4B Instruct (GGUF)** → Generates code and explanations using **llama.cpp** with **llama-cpp-python**.
* **Response Processing** → Formats generated code, explanations, and markdown for readability.
* **Final Output** → Returns high-quality code, debugging suggestions, documentation, or programming guidance to the user.


## Why use `llama.cpp` with Gemma 4?

GemmaCode  is designed to provide **fast, efficient, and accessible AI-assisted programming** while remaining lightweight enough to run on modest hardware.

* **Efficient local inference** → `llama.cpp` with the GGUF version of **Google Gemma 4 E4B Instruct** significantly reduces memory requirements, making the assistant practical on consumer hardware and resource-constrained environments.
* **High-quality code generation** → Gemma 4 is responsible for understanding programming requests, generating code, explaining concepts, debugging errors, and assisting with software development tasks.
* **Scalable architecture** → The inference engine is separated from the application layer, making it straightforward to integrate future capabilities such as Retrieval-Augmented Generation (RAG), tool calling, project-aware coding, and file analysis.
* **Privacy-first execution** → Since inference can run locally, source code and user prompts do not have to be sent to external cloud AI services.
* **Cloud-ready deployment** → Although optimized for local execution, the same `llama.cpp` backend can be deployed behind a FastAPI service and hosted on cloud infrastructure, allowing web and desktop clients to access the model through a standard API.

This architecture enables GemmaCode to deliver reliable AI coding assistance today while providing a flexible foundation for future enhancements such as project-aware development, documentation retrieval, and autonomous coding workflows.


## Tech Stack

| Layer                        | Technology                                                                                                       |
| ---------------------------- | -------------------------------------------------------------------------------------------------------
|
| **Programming Language**     | Python                                                                                                           |
| **Foundation Model**         | Google Gemma 4 E4B Instruct                                                                                      |
| **Model Format**             | GGUF (Q4_0 Quantization)                                                                                         |
| **Inference Engine**         | llama.cpp                                                                                                        |
| **Python Inference Library** | llama-cpp-python                                                                                                 |
| **Development Environment**  | Google Colab                                                                                                     |
| **Model Storage**            | Google Drive / Local Storage                                                                                     |
| **Backend (Planned)**        | Django rest framework                                                                                                          |
| **Frontend (Planned)**       | Next.js and Tailwind                                                                                                   |
| **Deployment (Planned)**     | Docker, Google Cloud, AWS, Azure, or any server capable of running `llama.cpp`                                   |
| **Future Enhancements**      | Retrieval-Augmented Generation (RAG), Tool Calling, Project-Aware Code Generation, Multi-file Code Understanding |

### Current Architecture

* **Inference:** Google Gemma 4 E4B Instruct (GGUF) running through **llama.cpp** with **llama-cpp-python**.
* **Development:** Built and tested in **Google Colab**, with the model stored in **Google Drive** for efficient reuse.
* **Optimization:** Uses **Q4_0 quantization** to reduce memory usage while maintaining strong code generation performance.
* **Deployment:** Designed for both **local execution** and **cloud-hosted APIs**, allowing integration with web, desktop, or mobile applications.


## 🚀 Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/<your-username>/NaijaDev-AI.git
cd NaijaDev-AI
```

---

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

or install the core packages manually:

```bash
pip install llama-cpp-python huggingface_hub hf_xet
```

---

### 3. Download the Gemma 4 Model

Download the **Google Gemma 4 E4B Instruct GGUF** model from Hugging Face.

```python
from huggingface_hub import hf_hub_download

model_path = hf_hub_download(
    repo_id="ggml-org/gemma-4-E4B-it-GGUF",
    filename="gemma-4-E4B-it-Q4_0.gguf",
)

print(model_path)
```

Alternatively, place the downloaded model inside:

```text
model/
└── gemma-4-E4B-it-Q4_0.gguf
```

---

### 4. Load the Model

```python
from llama_cpp import Llama

llm = Llama(
    model_path="model/gemma-4-E4B-it-Q4_0.gguf",
    n_gpu_layers=-1,
    n_ctx=4096,
    verbose=False,
)
```

---

### 5. Test the Model

```python
response = llm.create_chat_completion(
    messages=[
        {
            "role": "user",
            "content": "Write a Python function that reverses a string."
        }
    ],
    max_tokens=256,
    temperature=0.2,
)

print(response["choices"][0]["message"]["content"])
```

---

## Requirements

* Python 3.10+
* Google Gemma 4 E4B Instruct (GGUF)
* `llama.cpp`
* `llama-cpp-python`
* Google Colab, Linux, macOS, or Windows
* NVIDIA GPU (recommended for faster inference) or CPU for local execution

---

## Deployment

GemmaCode is designed to run:

* 💻 Locally on Windows, Linux, or macOS
* ☁️ On cloud virtual machines 
* 🌐 Behind a web application built with React or Next.js
* 🔌 As a REST API for integration into desktop, web, or mobile applications


## Request Routing

When a user submits a programming request, GemmaCode intelligently routes it through the appropriate processing pipeline.

| User Request                                                            | Processing                                                                                 |
| ----------------------------------------------------------------------- | -------------------------------------------------------------|
| **Code Generation** — "Build a React login page."                       | Gemma 4 generates production-ready code.                                                   |
| **Code Debugging** — "Why is this Python code throwing an error?"       | Gemma 4 analyzes the code, identifies issues, and suggests fixes.                          |
| **Code Explanation** — "Explain this JavaScript function."              | Gemma 4 provides a detailed, line-by-line explanation.                                     |
| **Code Optimization** — "Make this function faster."                    | Gemma 4 refactors and optimizes the implementation while preserving functionality.         |
| **Project Scaffolding** — "Create a FastAPI backend."                   | Gemma 4 generates the initial project structure and boilerplate code.                      |
| **Documentation Generation** — "Write documentation for this function." | Gemma 4 produces clear comments and technical documentation.                               |
| **Future RAG Query** — "How do I use this project function?"            | Retrieve relevant project documentation before generating a grounded response. *(Planned)* |
| **General Programming Questions**                                       | Gemma 4 answers using its programming knowledge and reasoning capabilities.                |

**Routing Principle:** Simple programming requests are sent directly to **Gemma 4** for inference. Future versions will automatically retrieve relevant project files, documentation, or coding standards through a **Retrieval-Augmented Generation (RAG)** pipeline before generating responses, improving accuracy for project-specific questions.


## Design Principles

* **Efficient Local Inference** — GemmaCode runs using the **Google Gemma 4 E4B Instruct GGUF** model powered by **llama.cpp**, enabling fast inference with reduced memory requirements and minimal hardware dependencies.

* **Privacy by Design** — User prompts and source code can be processed locally, reducing reliance on external cloud AI services and helping protect sensitive codebases.

* **Reliable Code Generation** — Every response is generated directly from **Gemma 4**, with future support for Retrieval-Augmented Generation (RAG) to ground answers in project documentation, codebases, and developer resources.

* **Resource Optimized** — Built around **Q4_0 quantization**, configurable context windows, and GPU acceleration where available, allowing the assistant to perform efficiently on consumer hardware.

* **Modular Architecture** — The application separates the user interface, inference engine, and future retrieval pipeline, making it straightforward to extend with APIs, tool calling, project-aware coding, and multi-file understanding.

* **Cloud-Ready Deployment** — Although optimized for local execution, the same inference backend can be deployed behind a FastAPI service using Docker on cloud infrastructure, enabling web, desktop, and mobile applications to interact with NaijaDev AI through a standard API.

* **Developer-Centric Experience** — Every feature is designed to improve developer productivity by generating code, explaining programming concepts, debugging errors, refactoring existing code, and accelerating software development workflows.
**Accessible AI coding assistance powered by Google Gemma 4—built for developers, students, and startups**

  ## License & Model Information

### Project Code

The NaijaDev AI (GemmaCode) application code is released under the license specified in this repository.

### AI Model

* **Foundation Model:** Google **Gemma 4 E4B Instruct**
* **Model Format:** GGUF (Q4_0 Quantization)
* **Inference Engine:** `llama.cpp`
* **Python Runtime:** `llama-cpp-python`

The Gemma 4 model is **not included** in this repository. Users must download the model separately from the official Hugging Face repository and comply with Google's **Gemma license and usage terms**.

### Third-Party Dependencies

GemmaCode is built on the following open-source technologies:

* **Google Gemma 4** — Foundation language model
* **llama.cpp** — High-performance GGUF inference engine
* **llama-cpp-python** — Python bindings for `llama.cpp`
* **Hugging Face Hub** — Model distribution and download
* **Python** — Core application runtime


