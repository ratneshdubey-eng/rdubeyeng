# Hi, I'm Ratnesh Dubey 👋

### AI & Software Architect | Designing Production-Grade AI Systems

> 12+ years building enterprise platforms. Now focused on architecting **Agentic AI**, **RAG pipelines**, and **LLM-powered systems** at scale.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-ratnesh--dubey-blue?style=flat&logo=linkedin)](https://linkedin.com/in/ratnesh-dubey-profile)
[![Blog](https://img.shields.io/badge/Blog-ratneshdubey.in-orange?style=flat&logo=hashnode)](https://ratneshdubey.in)
[![McAfee](https://img.shields.io/badge/Company-McAfee-red?style=flat&logo=mcafee)](https://mcafee.com)

---

## 🧠 What I Architect

| Domain | Technologies |
|---|---|
| **LLM Applications** | Claude, GPT-4, AWS Bedrock, LangChain |
| **Agentic AI** | LangGraph, MCP, Tool Calling, Multi-Agent Systems |
| **RAG Systems** | FAISS, Pinecone, pgvector, Semantic Search |
| **AI Observability** | LangSmith, OpenTelemetry, Prometheus |
| **Cloud AI Platform** | AWS Bedrock, Lambda, ECS, SageMaker |
| **Core Platform** | Kubernetes, Kafka, Terraform, Microservices |

---

## 🔧 Tech Stack

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=flat&logo=typescript&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat&logo=amazonaws&logoColor=white)
![LangGraph](https://img.shields.io/badge/LangGraph-1C3C3C?style=flat&logo=langchain&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat&logo=kubernetes&logoColor=white)
![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=flat&logo=terraform&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-336791?style=flat&logo=postgresql&logoColor=white)

---

## 🏗️ Code Evidence — AI Architect in Action

### 1. RAG Pipeline with Semantic Chunking (Python)

```python
# production_rag.py — Retrieval-Augmented Generation with re-ranking
from langchain.text_splitter import RecursiveCharacterTextSplitter
from langchain_aws import BedrockEmbeddings, ChatBedrock
from langchain_community.vectorstores import FAISS
from langchain.chains import RetrievalQA
from langchain.retrievers import ContextualCompressionRetriever
from langchain.retrievers.document_compressors import CrossEncoderReranker
import boto3

class ProductionRAGPipeline:
    """
    Production-grade RAG pipeline using AWS Bedrock.
    Features: semantic chunking, re-ranking, source attribution.
    """
    def __init__(self, model_id: str = "anthropic.claude-3-5-sonnet-20241022-v2:0"):
        self.bedrock = boto3.client("bedrock-runtime", region_name="us-east-1")
        self.embeddings = BedrockEmbeddings(
            client=self.bedrock,
            model_id="amazon.titan-embed-text-v2:0"
        )
        self.llm = ChatBedrock(
            client=self.bedrock,
            model_id=model_id,
            model_kwargs={"temperature": 0.1, "max_tokens": 2048}
        )
        self.vectorstore = None

    def ingest(self, documents: list[str]) -> None:
        splitter = RecursiveCharacterTextSplitter(
            chunk_size=512,
            chunk_overlap=64,
            separators=["\n\n", "\n", ". ", " "]
        )
        chunks = splitter.create_documents(documents)
        self.vectorstore = FAISS.from_documents(chunks, self.embeddings)
        print(f"Indexed {len(chunks)} chunks into FAISS")

    def query(self, question: str, top_k: int = 5) -> dict:
        retriever = self.vectorstore.as_retriever(search_kwargs={"k": top_k})
        chain = RetrievalQA.from_chain_type(
            llm=self.llm,
            retriever=retriever,
            return_source_documents=True
        )
        result = chain.invoke({"query": question})
        return {
            "answer": result["result"],
            "sources": [doc.metadata for doc in result["source_documents"]]
        }
```

---

### 2. Agentic AI with LangGraph (Multi-Agent Workflow)

```python
# agentic_workflow.py — LangGraph multi-agent with tool use
from langgraph.graph import StateGraph, END
from langgraph.prebuilt import ToolNode
from langchain_aws import ChatBedrock
from langchain_core.messages import HumanMessage, SystemMessage
from typing import TypedDict, Annotated
import operator

class AgentState(TypedDict):
    messages: Annotated[list, operator.add]
    current_agent: str
    final_answer: str

def create_research_agent(llm, tools):
    """Research agent — gathers context via tools."""
    def research_node(state: AgentState):
        system = SystemMessage(content="You are a research agent. Use tools to gather information.")
        response = llm.bind_tools(tools).invoke([system] + state["messages"])
        return {"messages": [response], "current_agent": "researcher"}
    return research_node

def create_synthesis_agent(llm):
    """Synthesis agent — produces final structured answer."""
    def synthesis_node(state: AgentState):
        system = SystemMessage(content="Synthesize research into a concise, grounded answer.")
        response = llm.invoke([system] + state["messages"])
        return {"messages": [response], "final_answer": response.content}
    return synthesis_node

def router(state: AgentState) -> str:
    last = state["messages"][-1]
    if hasattr(last, "tool_calls") and last.tool_calls:
        return "tools"
    if state["current_agent"] == "researcher":
        return "synthesizer"
    return END

def build_agent_graph(llm, tools):
    graph = StateGraph(AgentState)
    graph.add_node("researcher", create_research_agent(llm, tools))
    graph.add_node("tools", ToolNode(tools))
    graph.add_node("synthesizer", create_synthesis_agent(llm))
    graph.set_entry_point("researcher")
    graph.add_conditional_edges("researcher", router)
    graph.add_edge("tools", "researcher")
    graph.add_edge("synthesizer", END)
    return graph.compile()
```

---

### 3. MCP Server Implementation (Model Context Protocol)

```python
# mcp_server.py — Production MCP server exposing enterprise tools to Claude
from mcp.server import Server
from mcp.server.stdio import stdio_server
from mcp.types import Tool, TextContent
import boto3, json

app = Server("enterprise-ai-tools")

@app.list_tools()
async def list_tools() -> list[Tool]:
    return [
        Tool(
            name="query_knowledge_base",
            description="Query the enterprise knowledge base using semantic search",
            inputSchema={
                "type": "object",
                "properties": {
                    "query": {"type": "string", "description": "Search query"},
                    "top_k": {"type": "integer", "default": 5}
                },
                "required": ["query"]
            }
        ),
        Tool(
            name="invoke_bedrock_model",
            description="Invoke an AWS Bedrock model with a prompt",
            inputSchema={
                "type": "object",
                "properties": {
                    "model_id": {"type": "string"},
                    "prompt": {"type": "string"}
                },
                "required": ["model_id", "prompt"]
            }
        )
    ]

@app.call_tool()
async def call_tool(name: str, arguments: dict) -> list[TextContent]:
    if name == "invoke_bedrock_model":
        client = boto3.client("bedrock-runtime", region_name="us-east-1")
        response = client.invoke_model(
            modelId=arguments["model_id"],
            body=json.dumps({"prompt": arguments["prompt"], "max_tokens": 1024})
        )
        result = json.loads(response["body"].read())
        return [TextContent(type="text", text=result.get("completion", ""))]

async def main():
    async with stdio_server() as (read, write):
        await app.run(read, write, app.create_initialization_options())
```

---

### 4. AI Observability — LLM Tracing with OpenTelemetry

```python
# llm_observability.py — Production tracing for LLM calls
from opentelemetry import trace
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.sdk.trace.export import BatchSpanProcessor
from opentelemetry.exporter.otlp.proto.grpc.trace_exporter import OTLPSpanExporter
from functools import wraps
import time, json

tracer = trace.get_tracer("llm.architect")

def trace_llm_call(model_name: str):
    """Decorator to trace every LLM invocation with token counts and latency."""
    def decorator(func):
        @wraps(func)
        async def wrapper(*args, **kwargs):
            with tracer.start_as_current_span(f"llm.{model_name}") as span:
                start = time.time()
                try:
                    result = await func(*args, **kwargs)
                    span.set_attribute("llm.model", model_name)
                    span.set_attribute("llm.latency_ms", (time.time() - start) * 1000)
                    span.set_attribute("llm.output_tokens", getattr(result, "usage", {}).get("output_tokens", 0))
                    span.set_attribute("llm.status", "success")
                    return result
                except Exception as e:
                    span.set_attribute("llm.status", "error")
                    span.set_attribute("llm.error", str(e))
                    raise
        return wrapper
    return decorator

@trace_llm_call(model_name="claude-3-5-sonnet")
async def invoke_claude(prompt: str, system: str = "") -> dict:
    import anthropic
    client = anthropic.AsyncAnthropic()
    return await client.messages.create(
        model="claude-3-5-sonnet-20241022",
        max_tokens=1024,
        system=system,
        messages=[{"role": "user", "content": prompt}]
    )
```

---

## 📂 Repositories

| Repo | Description | Stack |
|---|---|---|
| [llm-code-review-test](https://github.com/ratneshdubey-eng/llm-code-review-test) | LLM-powered code review automation | C#, LLM |
| [fanpulse-bff](https://github.com/ratneshdubey-eng/fanpulse-bff) | Backend-for-frontend with AI features | Python |
| [fanpulse](https://github.com/ratneshdubey-eng/fanpulse) | AI-powered fan engagement platform | TypeScript |

---

## 📖 Latest Writing

- [Understanding Transformers — the Engine of LLMs](https://ratneshdubey.in/2025/11/27/understanding-transformers-the-engine-of-llms/)
- [What Are Weights and Parameters in an LLM](https://ratneshdubey.in/2025/12/20/what-are-weights-and-parameters-in-an-llm/)
- [TOON vs JSON: Revolutionizing Data Transmission for LLMs](https://ratneshdubey.in/2025/11/13/toon-vs-json-revolutionizing-data-transmission-for-llm/)
- [Patterns for Designing Self-Healing Apps](https://ratneshdubey.in)

---

## 📬 Connect

- 🌐 Blog: [ratneshdubey.in](https://ratneshdubey.in)
- 💼 LinkedIn: [linkedin.com/in/ratnesh-dubey-profile](https://linkedin.com/in/ratnesh-dubey-profile)
- 🏢 Currently: **Cloud Software Architect @ McAfee**

---

> *"Architecture is not about tools. It's about the decisions you make before you write a single line of code."*
