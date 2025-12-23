# Multi-Agent LLM Automated Marking System

> A web-based, modular, AI-powered system for automated, fair, and auditable assessment of student submissions in higher education. The system leverages multiple specialized agents, historical academic and professional records, and structured rubrics to provide explainable grades and feedback.

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Features](#features)
3. [System Architecture](#system-architecture)
4. [File Structure](#file-structure)
5. [Installation](#installation)
6. [Usage](#usage)
7. [Deployment](#deployment)
8. [Technologies](#technologies)
9. [Future Enhancements](#future-enhancements)
10. [License](#license)

---

## Project Overview

This project implements a **multi-agent AI marking system** that provides:

- Automated grading of academic assignments using LLMs.
- Contextualized evaluation using **student submissions, historical grades, and professional records**.
- **Explainable feedback** with evidence references for each rubric criterion.
- **Bias and fairness analysis** with optional human oversight.
- Appeals handling and human-in-the-loop intervention.

The system is designed for **scalability, modularity, and responsible AI** principles.

---

## Features

- **Multi-Agent Architecture**: Retrieval, Context/Evidence Builder, Grading, Bias & Fairness, Appeals Agents.
- **Dynamic Workflows**: Orchestrator allows flexible execution of agents in any sequence.
- **Explainable Outputs**: Feedback includes evidence pointers and reasoning (audit logs).
- **Audit & Provenance**: Full logging of prompts, context, and outputs for reproducibility.
- **Human-in-the-Loop Support**: Educators can review, override, or edit grades.
- **Frontend Dashboard**: Students and instructors view submissions, marks, and appeals.
- **Persistent Storage**: Postgres DB for records; Vector DB for semantic retrieval; cloud storage for file uploads.

---

## System Architecture

**High-Level Flow:**

1. Student submits an assignment via frontend.
2. Orchestrator selects the agent workflow (dynamic).
3. **Agents execute sequentially or in parallel**:
   - Retrieval Agent → Context Agent → Grading Agent → Bias Agent → Appeals Agent.
4. Results are stored in Postgres, embeddings in Vector DB, audit logs stored for reproducibility.
5. Feedback is returned to the frontend dashboard, with optional human review.

**Deployment Overview:**

- Backend: Flask API + Orchestrator
- Worker: Celery/RQ for async agent execution
- Frontend: React application
- Databases: Postgres (records), Vector DB (document embeddings)
- Cache/Broker: Redis for queue management
- Storage: Cloud object storage for PDFs/DOCX
- Hosting: Render, AWS, or other cloud services

---

## File Structure

## Installation

1. **Clone the repository**

   git clone https://github.com/your-username/llm-multi-agent-marking.git
   cd llm-multi-agent-marking

2. **Backend setup**

   cd backend
   python -m venv venv
   source venv/bin/activate # Linux / macOS
   venv\Scripts\activate # Windows
   pip install -r requirements.txt

3. **Frontend setup**

   cd frontend
   npm install
   npm run build

4. **Environment Variables**

   FLASK_ENV=development
   DATABASE_URL=postgres://username:password@host:port/dbname
   REDIS_URL=redis://localhost:6379
   OPENAI_API_KEY=your_openai_api_key
   VECTOR_DB_API_KEY=your_vector_db_key

## Usage

1. **Run backend API**

   cd backend
   flask run

# or using gunicorn

    gunicorn wsgi:app

2. **Start Worker**

   cd backend
   rq worker default

3. **Serve Frontend**

   - Either via Flask static files or npm start in frontend/

4. **Submit Assignment**

   - Navigate to /submit
   - Upload PDF/DOCX
   - Choose workflow (e.g., full assessment or quick marking)
   - View results on dashboard

## Deployment

- Frontend: Static web service or served via backend
- Backend: Web service + Worker service (Render)
- Databases: Postgres & Vector DB (cloud-hosted)
- Queue Broker: Redis (managed service)
- File Storage: Cloud (S3 / Render storage)

## Technologies

- Backend: Python, Flask, SQLAlchemy, RQ/Celery
- Frontend: React, TypeScript
- Database: Postgres, Vector DB (Pinecone/Milvus/Weaviate)
- Queue/Broker: Redis
- AI/LLM: OpenAI GPT / local LLM models
- Storage: Cloud object storage (S3/MinIO)
- Deployment: Render / Docker

## Future Enhancements

- Add multi-lingual support for submissions
- Integrate self-supervised feedback agents
- Add real-time marking progress with websockets
- Expand analytics dashboard for instructor insights

## License

MIT License © 2025 Divya Lamichhane
