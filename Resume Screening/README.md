
# AI Resume Screening & Candidate Ranking

An AI-powered resume screening and candidate ranking automation built using **n8n, AI Agents, OpenAI, Gmail, and Google Sheets**.

The system automatically extracts information from submitted resumes, compares the candidate's profile with the provided job description, calculates a candidate score, classifies the candidate, stores the result in Google Sheets, and sends an automated email to the candidate.

---

## 🚀 Project Overview

Recruiters often need to manually review a large number of resumes for a single job opening. This process can be time-consuming and inconsistent.

This project automates the initial resume screening process using an **AI Agent**.

The workflow:

1. Receives a resume through an n8n form.
2. Extracts the resume content from the uploaded PDF.
3. Sends the resume information and job requirements to an AI Agent.
4. The AI Agent analyzes the candidate against the job description.
5. Generates a candidate score and matching information.
6. A Switch node classifies the candidate based on the score.
7. Candidate details are stored in Google Sheets.
8. An automated email is sent to the candidate.

---

## 🏗️ Workflow Architecture

```text
Candidate
    |
    v
On Form Submission
    |
    v
Extract from PDF
    |
    v
AI Agent
    |
    +---- OpenAI Chat Model
    |
    +---- Structured Output Parser
    |
    v
Switch
    |
    +---- Shortlisted
    |        |
    |        v
    |   Google Sheets
    |        |
    |        v
    |      Gmail
    |
    +---- Under Screening
    |        |
    |        v
    |   Google Sheets
    |        |
    |        v
    |      Gmail
    |
    +---- Rejected
             |
             v
        Google Sheets
             |
             v
           Gmail
