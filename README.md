# "What Would Lee Kuan Yew Do?" Chatbot

An exported workflow for a persona chatbot that answers questions in the voice of Lee Kuan Yew. This repository contains the workflow definition (platform export) and the source knowledge base used by the workflow.

This project is an asset bundle for a hosted chatbot platform (see the Live Demo link below). The repository does not contain a local application server or build scripts.

## Features
- Persona-based LLM prompt that instructs the model to emulate Lee Kuan Yew's style.
- Retriever-enabled workflow that uses a provided PDF knowledge base for factual grounding.
- Workflow export referencing a marketplace LLM plugin and a specific model: `gemini-3.5-flash-lite`.
- Public demo link to try the chatbot online.

## System Architecture
This repository is a workflow export for a hosted chatbot platform. The runtime flow (as described in `LKY Chatbot.yml`):
- User Input -> LLM node (system persona prompt + retriever) -> Answer node

Components and roles:
- Workflow (LKY Chatbot.yml): Defines the nodes, prompt template, model, and features.
- Knowledge Base (Lee_Kuan_Yew.pdf): Source material intended for retrieval/grounding.
- Hosted platform (external): The workflow is intended to be run/imported on a platform (e.g., the one that produced the YAML or Udify) that provides the LLM model and retriever infrastructure.

## Tech Stack
- Workflow / export format: YAML (platform-specific workflow export)
- Model provider / plugin: LangGenius marketplace plugin referencing Google Gemini (see the YAML)
- Content / knowledge source: PDF (Lee_Kuan_Yew.pdf)
- Documentation: Markdown (README.md)

## Project Structure
```
.
├── README.md                 # This file — cleaned and expanded
├── LKY Chatbot.yml           # Workflow export (nodes, prompt, model settings)
└── Lee_Kuan_Yew.pdf          # Knowledge base referenced by the workflow
```

- `LKY Chatbot.yml` — core artifact: the exported workflow that encodes the persona prompt, model selection, retriever flag, and graph nodes. Import this file into the platform that supports such workflow imports.
- `Lee_Kuan_Yew.pdf` — knowledge source (memoirs, speeches) used by the workflow for grounding answers.

## Requirements
- No local runtime found in this repository.
- To run the workflow you need:
  - Access to the platform that supports this workflow export (the demo link suggests the workflow runs on a hosted chatbot service).
  - Access/credentials to the model provider if hosting/running on the target platform (the YAML references `gemini-3.5-flash-lite` with a LangGenius plugin).
- Optional: an account on the platform (Udify / the marketplace used) to import workflows.

## Installation / Usage (how to try)
1. Try the public demo in a browser:
   - Public demo: https://udify.app/chat/CI9O3BNZN92uSsVm
2. To import locally into a compatible platform:
   - Download `LKY Chatbot.yml` and `Lee_Kuan_Yew.pdf`.
   - Use the target platform's "import workflow" or "create from YAML" feature to upload `LKY Chatbot.yml`.
   - If the platform requires it, upload the PDF as the knowledge base / retriever content or configure the retriever to point to this document.
   - Ensure the platform has access to the named model or a compatible model; provide any required credentials on the platform.

No local CLI or server commands are provided in the repository.

## Configuration
- All configuration for the chatbot (model name, prompt template, retriever, features) lives inside `LKY Chatbot.yml`.
- The export contains the model name `gemini-3.5-flash-lite` and a marketplace dependency for `langgenius/gemini`.
- There are no `.env` files or secrets in the repository. Do not commit secrets to source control — supply them via your hosting platform when required.

## API Documentation
- This repository does not include REST API code or endpoint definitions. The workflow is intended to run within a hosted platform that provides an API or UI.

## Usage examples
- Open the demo link and ask: "How would Lee Kuan Yew respond to a question about economic policy?" The model will reply using the persona defined in the system prompt embedded in the YAML.

### Sample Answer (example)
**User:** "How should a small country approach economic growth in an uncertain global environment?"

**Example model reply (persona-style):**
> Focus on national survival first. Prioritise long-term stability over short-term popularity: build strong institutions, invest in education and technical skills, and pursue pragmatic industrial policy that matches your country's comparative advantages. Avoid reckless debt and let meritocracy guide leadership and public service. Trade and openness are important, but sovereignty and social cohesion must not be sacrificed for transient gains.

This example is a short, illustrative reply inspired by the persona prompt in the workflow; it is not an actual model output recorded from the hosted demo.

## Troubleshooting
- YAML import fails: ensure the target platform supports the same workflow format and that you import both the YAML and knowledge base assets where the platform expects them.
- Retriever returns no results: verify the PDF was uploaded to the platform's document store and indexed for retrieval.
- Model not available: the referenced model `gemini-3.5-flash-lite` may require platform access or specific marketplace plugin — use a compatible model on your platform.

## Security Notes
- This repository does not include API keys, credentials, or secrets.
- If you host the workflow, keep model/provider credentials secure and avoid committing them.
- Be mindful that persona prompts can produce sensitive opinions; include safeguards and human review for public deployments.

## Development
- This repo is an export artifact; to develop further you can:
  - Extract text from `Lee_Kuan_Yew.pdf` and create structured documents or embeddings for a RAG pipeline.
  - Modify the system prompt inside the workflow to adjust persona tone.
  - Add integration code (a server or UI) if you want a self-hosted deployment (not provided here).

## Contributing
- If you'd like contributions, consider adding:
  - A LICENSE file.
  - CONTRIBUTING.md with steps to import and test the workflow on the target platform.
  - Scripts or instructions to convert the PDF into indexed documents/embeddings.

## License
- No license file found in the repository. Add a LICENSE if you intend to allow reuse under a specific license.

## Author / Maintainer
- Repository owner: katarizkyo99 (GitHub)
