# UdaPlay - AI Game Research Agent

UdaPlay is an AI research agent for video games. It answers questions about games,
platforms, release years and publishers. It first tries a local vector database (RAG),
and falls back to a web search when the local data is not enough.

## What it does

- **Part 1 (RAG):** loads the game JSON files into a ChromaDB vector database and runs semantic search.
- **Part 2 (Agent):** an agent with three tools:
  - `retrieve_game` - search the vector database
  - `evaluate_retrieval` - check if the results are good enough
  - `game_web_search` - search the web (Tavily) when they are not
  - plus long-term memory (`search_memory` / `register_memory`) so it can reuse web answers later.

## Getting Started

1. Create a `.env` file in the project folder:
   ```
   OPENAI_API_KEY="your key"
   CHROMA_OPENAI_API_KEY="your key"
   TAVILY_API_KEY="your key"
   ```
2. Run `Udaplay_01_solution_project.ipynb` first - it builds the vector database (`chromadb/`).
3. Then run `Udaplay_02_solution_project.ipynb` - it uses that database and runs the agent.

### Dependencies

- Python 3.11+
- chromadb >= 1.0.4
- openai >= 1.73.0
- pydantic >= 2.11.3
- python-dotenv >= 1.1.0
- tavily-python >= 0.5.4

## Testing

There are no automated tests. The notebooks show it working:

- Part 1 prints semantic search results for a few queries.
- Part 2 runs three example questions (Pokémon, Mario, Mortal Kombat) and shows the
  reasoning, the tools used and the final answer with sources.
- The long-term memory section proves the agent learns from a web search: it answers a
  question via the web, then answers the same question in a new session using only memory.

## Built With

- [ChromaDB](https://www.trychroma.com/) - vector database
- [OpenAI](https://openai.com/) - LLM and embeddings
- [Tavily](https://tavily.com/) - web search

## License

[License](../LICENSE.md)
