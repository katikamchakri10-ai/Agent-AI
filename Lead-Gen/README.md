# AI Lead Qualification & Email Automation

## Description

This project is an AI-powered lead qualification and automation workflow built using **n8n and OpenAI**.

The system collects lead information through an online form and sends the submitted data to an **AI Agent** for analysis. The AI evaluates the lead based on predefined criteria and generates a lead score. A **Switch node** then routes the lead to the appropriate workflow based on the result.

Depending on the lead category, the system automatically stores the lead information in **Google Sheets** and sends personalized email notifications using **Gmail**, reducing manual lead-processing work.

## Architecture

```text
                  Lead / User
                       │
                       ▼
              ┌─────────────────┐
              │  Form Submission │
              └────────┬────────┘
                       │
                       ▼
                ┌─────────────┐
                │   AI Agent  │
                └──────┬──────┘
                       │
              ┌────────┴────────┐
              │                 │
              ▼                 ▼
       OpenAI Chat Model   Structured Output
                                Parser
                       │
                       ▼
                ┌─────────────┐
                │ Switch Node  │
                └──────┬──────┘
                       │
          ┌────────────┼────────────┐
          │            │            │
          ▼            ▼            ▼
      Shortlisted   Under Review  Rejected
          │            │            │
          ▼            ▼            ▼
        Gmail      Google Sheets  Google Sheets
                       │            │
                       ▼            ▼
                     Gmail        Gmail
                       │            │
                       └─────┬──────┘
                             ▼
                     Automated Response
