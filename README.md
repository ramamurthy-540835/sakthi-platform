# Sakthi Platform

## Overview
The Sakthi Platform is an enterprise-grade, AI-powered system designed to transform natural language inputs into actionable outputs. At its core is the MCP Language (Sakthi), a specialized framework for designing and executing Model Context Protocols (MCP) in Natural Language Processing. It provides a structured approach to manage context-aware workflows, semantic parsing, and seamless integration with Large Language Models (LLMs) for context-driven decision-making and language transformations. Built with Python, DeepSeek LLM, ChromaDB, and LangGraph, Sakthi delivers scalable, context-aware solutions for schema transformation, document processing, and workflow orchestration, complete with real-time monitoring, dynamic rule processing, and multi-format outputs.

## Business Problem
Modern enterprises face significant challenges in converting unstructured natural language data or complex domain-specific requests into actionable, structured outputs. This includes tasks such as migrating database schemas between different platforms, extracting specific information from diverse document types (PDFs, spreadsheets), and orchestrating complex workflows based on high-level natural language instructions. Manual approaches are slow, error-prone, and lack scalability and context-awareness. The Sakthi Platform addresses these challenges by providing an automated, AI-driven solution that understands natural language intent, leverages historical context, and generates precise, actionable outputs across various enterprise use cases.

## Key Capabilities
*   **Natural Language Interface**: Process complex tasks and queries using plain English, such as "Convert Oracle HR schema to BigQuery," "Extract revenue data from this PDF," or "Monitor competitor pricing daily."
*   **AI-Powered Processing**: Utilizes advanced LLMs like DeepSeek LLM (e.g., DeepSeek-Coder-6.7B, Codestral-22B) for intent recognition, SQL generation, data transformation, and code-related tasks.
*   **Context-Aware Workflows (RAG)**: Leverages ChromaDB for Retrieval-Augmented Generation (RAG) to incorporate historical context, past interactions, and relevant data, ensuring smarter and more accurate results.
*   **Dynamic Rule Processing**: Applies predefined business rules from a `rules.csv` file for conditional logic, SQL validations, and data integrity checks.
*   **Batch Processing**: Efficiently handles large datasets and complex operations, such as processing up to 1000 target fields simultaneously with the `EnhancedTargetProcessor`.
*   **Multi-format Outputs**: Generates diverse output formats including JSON, SQL scripts, CSV, and API-ready data structures, adaptable to various downstream systems.
*   **Workflow Orchestration & Monitoring**: Employs LangGraph to orchestrate complex AI workflows, monitor progress, and manage state across multi-step processes.
*   **Document Processing**: Capable of handling multi-format documents (PDF, XLSX, CSV) for data extraction and analysis.
*   **Enterprise-Grade Deployment**: Designed for robust deployment, supporting Dockerization, Kubernetes readiness, Nginx proxying, and WebSocket-based real-time updates.
*   **Backend Services/APIs**: Provides a well-defined FastAPI backend for programmatic access and integration.
*   **Web Interface**: Features an interactive Next.js dashboard for user interaction and visualization.

## Architecture
The Sakthi Platform follows a modular, microservices-oriented architecture, integrating several key components orchestrated by LangGraph.
1.  **User Interface (web-interface)**: A Next.js frontend provides the primary interaction point for users, submitting queries or uploading documents.
2.  **Backend (backend)**: A FastAPI application serves as the API gateway, handling requests from the frontend, orchestrating the processing flow, and interacting with other services. It exposes endpoints for natural language queries, document uploads, and result retrieval.
3.  **Sakthi Language Engine (sakthi-language)**: The core engine for the MCP Language, responsible for parsing natural language inputs, identifying intent, and structuring tasks. It drives the Model Context Protocol.
4.  **GenAI Modeling Agent (genai-modeling-agent)**: Integrates with LLMs (e.g., DeepSeek LLM via `sakthi-llm-integration`) to perform tasks like SQL generation, data transformation, and intent recognition. LangGraph orchestrates these AI agents for complex workflows.
5.  **Document Processor (document-processor)**: A dedicated service for parsing and extracting information from various document formats (PDF, XLSX, CSV).
6.  **ChromaDB (chromadb)**: Serves as the vector database for Retrieval-Augmented Generation (RAG), storing historical context, domain knowledge, and past interaction data to enhance LLM responses and maintain context.
7.  **Output & Storage**: Generated outputs (JSON, SQL, CSV) are stored in the `output/` directory, while input uploads are managed in `uploads/`. Context and historical data persist in ChromaDB.
8.  **Deployment**: Services are containerized with Docker and can be deployed using Docker Compose for local environments or Kubernetes for scalable, production-grade deployments, often fronted by Nginx.

## Tech Stack
*   **Core Language**: Python
*   **LLMs**: DeepSeek LLM (e.g., DeepSeek-Coder-6.7B, Codestral-22B)
*   **Vector Database**: ChromaDB
*   **Workflow Orchestration**: LangGraph
*   **Backend Framework**: FastAPI
*   **Frontend Framework**: Next.js
*   **Package Management (Frontend)**: Node.js / npm
*   **Containerization**: Docker
*   **Orchestration**: Kubernetes
*   **Web Server/Proxy**: Nginx
*   **Real-time Communication**: WebSockets

## Repository Structure

```plaintext
sakthi-platform/
├── .gitignore
├── LICENSE
├── README.md
├── automated_setup_script.py # Placeholder or utility script
├── backend/                  # FastAPI backend and API endpoints
│   ├── main.py
│   ├── api/
│   ├── requirements.txt
│   └── Dockerfile
├── config/                   # Configuration files and environment variables
│   ├── prompt_template.json
│   └── .env
├── core.py                   # Potentially a core utility script or part of Sakthi Language
├── deployment/               # Deployment configurations (Docker, Kubernetes, Nginx)
│   ├── docker-compose.yml
│   ├── kubernetes/
│   │   └── sakthi-platform.yaml
│   ├── nginx.conf
│   └── launch_enhanced_llm_servers.sh # LLM server startup script
├── docs/                     # Project documentation
├── document-processor/       # Service for handling multi-format documents (PDF, XLSX, CSV)
│   ├── processor.py
│   └── Dockerfile
├── genai-modeling-agent/     # AI agents with AutoGen + LangGraph for LLM workflows
│   ├── agent_system.py
│   └── Dockerfile
├── logs/                     # Log storage
├── output/                   # Generated outputs (JSON, SQL, CSV)
├── sakthi-language/          # Core Sakthi Engine (MCP Language implementation)
│   └── core.py
├── sakthi-llm-integration/   # Integration layer for LLMs (e.g., DeepSeek)
│   └── llm_provider.py
├── sakthi_architecture.svg   # Visual representation of the architecture
├── storage/                  # General data storage
├── tests/                    # Unit and integration tests
├── uploads/                  # User uploaded files (PDF, XLSX, CSV)
└── web-interface/            # Next.js frontend
    ├── pages/
    ├── components/
    │   └── Dashboard.jsx
    ├── package.json
    └── Dockerfile
```

**Artifact-to-File Mapping:**

| Artifact Name                           | File Location                             |
| :-------------------------------------- | :---------------------------------------- |
| Sakthi Language - Core Implementation   | `sakthi-language/core.py`                 |
| Document Processing Layer               | `document-processor/processor.py`         |
| GenAI Modeling Agent                    | `genai-modeling-agent/agent_system.py`    |
| DeepSeek LLM Integration                | `sakthi-llm-integration/llm_provider.py`  |
| FastAPI Backend                         | `backend/main.py`                         |
| Next.js Web Interface                   | `web-interface/components/Dashboard.jsx`  |
| Environment Configuration               | `config/.env`                             |
| Prompt Template                         | `config/prompt_template.json`             |
| Docker Compose Configuration            | `deployment/docker-compose.yml`           |
| Kubernetes Manifests                    | `deployment/kubernetes/sakthi-platform.yaml` |
| LLM Server Launch Script                | `deployment/launch_enhanced_llm_servers.sh` |

## Local Setup
To run the Sakthi Platform locally for development or testing:

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/ramamurthy-540835/sakthi-platform.git
    cd sakthi-platform
    ```

2.  **Set up Python backend environment:**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate
    pip install -r backend/requirements.txt
    ```

3.  **Install frontend dependencies:**
    ```bash
    cd web-interface
    npm install
    cd .. # Return to root
    ```

4.  **Configure environment variables:**
    Create a `.env` file in the `config/` directory based on `config/.env.example` (if available) and fill in necessary LLM API keys or other service endpoints.

5.  **Launch LLM servers:**
    The platform relies on local LLM servers for DeepSeek models. Use the provided script to start them.
    ```bash
    bash deployment/launch_enhanced_llm_servers.sh
    ```
    *   This script assumes `llama_cpp.server` is installed and models like `deepseek-coder-6.7b-instruct` and `codestral-22b` are accessible at specified paths (`/mnt/modelslist/`). Adjust paths as necessary for your environment.

6.  **Run services locally:**
    *   **Backend (FastAPI):**
        ```bash
        cd backend
        python main.py
        ```
    *   **Frontend (Next.js):**
        ```bash
        cd web-interface
        npm run dev
        ```
    Access the Web Interface at `http://localhost:3000` and API documentation at `http://localhost:8000/docs`.

## Deployment
The Sakthi Platform supports both Docker-based container deployment and Kubernetes orchestration for scalable production environments.

### Docker Deployment
For a consolidated deployment using Docker Compose:

1.  **Build and start all services:**
    Ensure Docker Desktop or a Docker engine is running.
    ```bash
    docker-compose -f deployment/docker-compose.yml up --build
    ```
    This command builds the necessary Docker images and starts the backend, frontend, document processor, and agent services.

2.  **Access Services:**
    *   **Web Interface**: `http://localhost:3000`
    *   **API Documentation**: `http://localhost:8000/docs`
    *   **LLM Endpoints**:
        *   DeepSeek-Coder: `http://localhost:11434/api/generate`
        *   Codestral: `http://localhost:11435/v1/chat/completions`

### Kubernetes Deployment
For a highly available and scalable deployment on a Kubernetes cluster:

1.  **Prepare Kubernetes Cluster:**
    Ensure your `kubectl` is configured to interact with your target Kubernetes cluster.
    ```bash
    kubectl create namespace sakthi-platform
    kubectl apply -f deployment/kubernetes/sakthi-platform.yaml -n sakthi-platform
    ```
    This command creates a dedicated namespace and deploys all defined services (backend, frontend, agents, document processor, ChromaDB) within it.

2.  **Monitor Deployment:**
    ```bash
    kubectl get pods -n sakthi-platform
    kubectl get services -n sakthi-platform
    ```
    Check logs and service statuses to ensure all components are running correctly. External access (e.g., via Ingress or NodePort) should be configured separately based on your cluster setup and `deployment/nginx.conf`.

## Demo Workflow
The Sakthi Platform streamlines complex tasks through natural language. Here are example workflows:

### 1. Schema Migration
**Scenario**: Convert an existing Oracle HR schema to a BigQuery-compatible schema.
1.  **Input**: User enters the query: "Convert Oracle HR schema to BigQuery."
2.  **Process**:
    *   The Sakthi Language Parser identifies the intent.
    *   DeepSeek LLM (e.g., DeepSeek-Coder-6.7B) is invoked to generate the corresponding BigQuery DDL (Data Definition Language) statements.
    *   The `EnhancedTargetProcessor` handles batch processing of target fields, ensuring accurate mapping and transformation logic.
    *   ChromaDB provides context from previous schema migrations or domain knowledge for more precise transformations.
    *   LangGraph orchestrates the steps, monitoring progress.
3.  **Output**: BigQuery DDL scripts, ETL scripts, and validation reports are generated and saved in the `output/` directory, available for download or API consumption.

### 2. Document Analysis & Data Extraction
**Scenario**: Extract quarterly revenue data by region from a financial report PDF or account details from an Excel sheet.
1.  **Input**: User uploads `financial_report.pdf` or `Account_Silver_Table_Column_List.xlsx` through the web interface.
2.  **Intent**: User specifies: "Extract quarterly revenue data by region."
3.  **Process**:
    *   The `document-processor/processor.py` service handles the uploaded file, parsing its content.
    *   DeepSeek LLM analyzes the parsed text/data to identify and extract the requested information.
    *   LangGraph monitors the extraction process, especially for large documents.
4.  **Output**: Structured data (e.g., JSON or CSV) containing the extracted revenue data by region is saved to `output/` and can be presented via the API or dashboard.

### 3. Web Data Integration & Monitoring
**Scenario**: Monitor competitor pricing changes daily from a specific webpage.
1.  **Input**: User provides the URL of the competitor pricing page and the intent: "Monitor pricing changes daily."
2.  **Process**:
    *   DeepSeek LLM, potentially integrated with external tools like SERPAPI, performs web scraping to retrieve pricing data.
    *   ChromaDB stores historical pricing data for comparison and context.
    *   The system schedules daily monitoring tasks.
    *   LangGraph orchestrates the recurring scraping and analysis workflow.
3.  **Output**: Automated trend analysis, pricing change alerts, or updated pricing data in `output/trends.json` or through real-time notifications via WebSockets.

## Future Enhancements
*   **Support for Additional LLMs**: Integration with a wider range of LLMs and foundation models to offer more flexibility and specialized capabilities.
*   **Advanced Monitoring and Analytics**: Develop more comprehensive dashboards for real-time performance monitoring, resource utilization, and detailed workflow analytics using tools like Prometheus/Grafana.
*   **Broader Data Source Integrations**: Expand connectivity to more databases (e.g., PostgreSQL, SQL Server), cloud storage services (S3, GCS), and enterprise applications.
*   **Enhanced Security Features**: Implement robust authentication, authorization, data encryption at rest and in transit, and role-based access control (RBAC).
*   **Improved UI/UX**: Further development of the Next.js web interface for an even more intuitive user experience, advanced visualization, and interactive workflow management.
*   **Explainability and Trustworthiness (XAI)**: Incorporate features to explain LLM decisions and generated outputs, fostering user trust and transparency.
*   **Self-Healing and Auto-Scaling**: Implement more advanced Kubernetes features for auto-scaling based on load and self-healing capabilities for increased resilience.
*   **Version Control for Protocols**: Introduce versioning for MCPs and prompt templates to manage changes and rollbacks effectively.