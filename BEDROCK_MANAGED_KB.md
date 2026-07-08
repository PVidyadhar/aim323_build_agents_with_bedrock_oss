# Bedrock Managed Knowledge Base Support

## Changes
- Added managed KB retrieval examples to notebook/tutorial materials
- New notebook cells demonstrate `managedSearchConfiguration` usage
- Added `AgenticRetrieveStream` example for agentic retrieval pattern
- Comparison section: managed vs vector retrieval (latency, simplicity, cost)
- Existing VECTOR retrieval notebook cells preserved with annotations

## Design
- MANAGED shown as alternative approach; existing VECTOR notebook unchanged
- Notebooks demonstrate end-to-end: create managed KB → ingest → retrieve
- AgenticRetrieveStream shown as recommended approach for agent-based architectures
- Backward compatible: existing VECTOR tutorial paths annotated, not removed

## API Shapes
- KB Creation: `type: MANAGED` + `managedKnowledgeBaseConfiguration.embeddingModelType: MANAGED`
- Retrieval: `managedSearchConfiguration` (not `vectorSearchConfiguration`)
- Agentic: `AgenticRetrieveStream` with `foundationModelType: MANAGED`, `rerankingModelType: MANAGED`

## Configuration
| Variable | Description | Default |
|---|---|---|
| KNOWLEDGE_BASE_TYPE | MANAGED or VECTOR | VECTOR |
| USE_AGENTIC_RETRIEVAL | Enable agentic retrieval | true |
| KNOWLEDGE_BASE_ID | Pre-created KB ID for tutorials | (required) |

## SDK Requirements
- boto3 >= 1.43 for managed search and agentic retrieval

## Required IAM Permissions
```json
{
  "Effect": "Allow",
  "Action": [
    "bedrock:Retrieve",
    "bedrock:AgenticRetrieveStream"
  ],
  "Resource": "arn:aws:bedrock:<region>:<account-id>:knowledge-base/<kb-id>"
}
```
