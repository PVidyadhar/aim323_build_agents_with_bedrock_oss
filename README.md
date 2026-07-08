## AIM323 Build Agentic Workflows with Amazon Bedrock and Open Source Frameworks

This repository contains code for Amazon Reinvent 2024 workshop on "Build Agentic Workflows with Amazon Bedrock and Open Source Frameworks". In this workshop, participants will get hands-on experience with building end-to-end agentic workloads using Amazon Bedrock, LangGraph, CrewAI and Ragas.

Labs Include

**Lab 1: AI Travel Assistant Use Case Introduction**
- Explore the travel assistant use case, covering the dataset on destinations, bookings, and preferences used throughout the labs. We’ll also set up Amazon Bedrock models to enable intelligent response generation and data retrieval, laying the groundwork for the assistant’s capabilities in upcoming labs.

**Lab 2: Building a Travel Planner with a Simple LangGraph**
- Learn the fundamentals of LangGraph, including nodes, edges, graphs, and memory concepts. Through a hands-on exercise, you’ll use these elements to build a simple travel recommendation system.

**Lab 3: Travel agent with tools**
- Build a travel chatbot agent designed to assist users in finding the ideal vacation destination. This agent will have access to various tools to search based on the user’s profile and the travel history of similar users. Additionally, it will use a retrieval tool to provide in-depth information on different cities across the United States

**Lab 4: Travel booking multi-agent**
- Implement a supervisor agentic pattern for handling travel bookings. Here, a central supervisor agent coordinates multiple specialized agents, each with its own dedicated scratchpad. The supervisor agent acts as a coordinator, assigning tasks to the Flight Agent and Hotel Agent based on their respective functions—such as searching, retrieving, changing, and canceling bookings. 
- Lab 6: Dream destination finder with CrewAI and Amazon Bedrock

**Lab 5: Dream Destination with CrewAI**
- Explore how to use the CrewAI framework with Amazon Bedrock to build an intelligent agent that can find dream travel destinations based on user preferences. The agent will utilize a large language model (LLM) and web search capabilities to research and recommend destinations that match the user's description.

**Lab 6: Evaluate Agents using ragas**
- Evaluate the effectiveness and accuracy of our multi-agent travel booking system using the [ragas library](https://docs.ragas.io/en/stable/). This lab will guide you through the process of evaluating agents' performance on various tasks, such as retrieving relevant information, generating accurate responses, and effectively handling user requests.

## Managed Knowledge Bases (New)

The knowledge base used in Lab 3 (travel agent with tools) can now leverage **Managed Knowledge Bases**, which let Bedrock handle embedding, storage, and retrieval automatically — no external vector store required.

To use a managed knowledge base with the workshop:
1. Create a Managed Knowledge Base in the [Amazon Bedrock console](https://console.aws.amazon.com/bedrock/)
2. Upload the workshop data files to the managed KB data source
3. Update the `knowledge_base_id` in the notebook to use your new managed KB ID

Managed KBs use `managedSearchConfiguration` instead of `vectorSearchConfiguration`:
```python
# Managed retrieval (recommended)
retrieval_config = {
    "managedSearchConfiguration": {
        "numberOfResults": 5
    }
}

# Vector retrieval (legacy)
retrieval_config = {
    "vectorSearchConfiguration": {
        "numberOfResults": 5
    }
}
```

> **Tip:** Managed KBs support agentic retrieval with intelligent query decomposition. Requires `boto3 >= 1.43`.

Managed KBs use a service-managed reranker by default (`rerankingModelType: MANAGED`). You can disable reranking (`NONE`) or use a custom model (`CUSTOM`).


**Required IAM Permissions:**
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

**Resources:** [Build a Managed KB](https://docs.aws.amazon.com/bedrock/latest/userguide/kb-build-managed.html) | [Retrieve API](https://docs.aws.amazon.com/bedrock/latest/userguide/kb-test-retrieve.html) | [Agentic Retrieval](https://docs.aws.amazon.com/bedrock/latest/userguide/kb-test-agentic.html)

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

MIT-0 License

