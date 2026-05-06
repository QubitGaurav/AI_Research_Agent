# AI Research Agent

A powerful AI research assistant powered by Claude 3.5 Sonnet and LangChain that conducts research using web search, Wikipedia lookup, and structured output generation.

## Overview

This project implements an intelligent research agent that:
- Accepts user queries about any topic
- Uses multiple tools to gather comprehensive research data
- Generates structured research responses with summaries, sources, and metadata
- Saves research outputs with timestamps for future reference

## Features

- **Claude AI Integration**: Leverages Claude 3.5 Sonnet for intelligent reasoning
- **Multi-Source Research**: Combines web search (DuckDuckGo) and Wikipedia for comprehensive coverage
- **Structured Output**: Returns validated JSON responses with topic, summary, sources, and tools used
- **Persistent Storage**: Automatically saves research results to file with timestamps
- **Error Handling**: Robust parsing and fallback mechanisms for reliable operation
- **Tool Calling Agent**: Uses LangChain's agent framework for intelligent tool selection

## Project Structure

```
AI_Agent/
├── main.py              # Main agent orchestration and LLM setup
├── tools.py             # Tool definitions (search, wiki, save)
├── requirements.txt     # Python dependencies
└── README.md           # Project documentation
```

## Installation

### Prerequisites
- Python 3.10+
- Anthropic API key

### Setup

1. Clone or download the repository
2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Create a `.env` file in the project root with your Anthropic API key:
```env
ANTHROPIC_API_KEY=your_api_key_here
```

## Usage

Run the AI research agent:
```bash
python main.py
```

When prompted, enter your research query:
```
What can i help you research? What are the latest developments in quantum computing?
```

### Output Format

The agent returns a structured response containing:
- **topic**: The research topic
- **summary**: Comprehensive summary of findings
- **sources**: List of sources consulted
- **tools_used**: Tools leveraged for the research (search, wiki, save)

### Example Output

```json
{
  "topic": "Quantum Computing Developments",
  "summary": "Recent breakthroughs in quantum computing include...",
  "sources": ["https://example.com", "Wikipedia: Quantum Computing"],
  "tools_used": ["search", "wiki", "save_text_to_file"]
}
```

## Tools Available

### 1. Web Search Tool
- **Provider**: DuckDuckGo
- **Function**: Searches the internet for current information
- **Use Case**: Finding latest news, articles, and web resources

### 2. Wikipedia Tool
- **Provider**: Wikipedia API
- **Function**: Queries Wikipedia for comprehensive topic information
- **Configuration**: Returns top 1 result with up to 100 characters of content
- **Use Case**: Getting structured, reliable background information

### 3. Save Tool
- **Function**: Persists research output to `research_output.txt`
- **Features**: Automatic timestamping, append mode for multiple queries
- **Use Case**: Building a research archive

## Dependencies

- **langchain**: Framework for building LLM applications
- **langchain-anthropic**: Anthropic Claude integration for LangChain
- **langchain-community**: Community tools and integrations
- **langchain-core**: Core LangChain functionality
- **pydantic**: Data validation and serialization
- **python-dotenv**: Environment variable management
- **duckduckgo-search**: Web search functionality
- **wikipedia**: Wikipedia API wrapper
- **langgraph**: Graph-based LLM orchestration

## Configuration

The agent is preconfigured with:
- **Model**: Claude 3.5 Sonnet (claude-3-5-sonnet-20241022)
- **Parser**: Pydantic-based output validation
- **Verbosity**: Enabled for debugging and monitoring

## Output Storage

Research results are automatically saved to `research_output.txt` with:
- Timestamp of when the research was conducted
- Full research output
- Append mode to maintain research history

## Error Handling

The application includes robust error handling:
- JSON parsing failures default to raw response output
- Tool execution errors are caught and reported
- Invalid queries are handled gracefully

## Requirements

See `requirements.txt` for the complete list of dependencies and their versions.

## Notes

- Ensure your Anthropic API key has sufficient quota
- Internet connection required for web search and Wikipedia queries
- Research outputs accumulate in `research_output.txt`; consider archiving or clearing periodically

## Future Enhancements

Potential improvements:
- Support for additional search providers
- Custom knowledge base integration
- Advanced query preprocessing and understanding
- Multi-query research workflows
- Result summarization and comparison
