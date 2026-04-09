# GraphLangchain - Neo4j Q&A System

A Python-based question-answering system that uses LangChain and Neo4j to provide intelligent responses about movie data. The system generates Cypher queries from natural language questions and executes them against a Neo4j graph database.

## Features

- **Natural Language Processing**: Convert user questions into accurate Cypher queries
- **Few-Shot Learning**: Uses example questions and queries to improve response quality
- **Neo4j Integration**: Direct integration with Neo4j graph database
- **LLM Support**: Powered by Groq's language models
- **Verbose Logging**: Detailed output of generated queries and results

## Prerequisites

- Python 3.8+
- Neo4j Database (local or cloud instance)
- Groq API Key

## Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/utssss117/GraphLangchain.git
   cd GraphLangchain
   ```

2. **Create a virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

## Setup

### 1. Environment Variables

Create a `.env` file in the project root:

```env
NEO4J_URI=neo4j+s://your-neo4j-uri
NEO4J_USERNAME=your-username
NEO4J_PASSWORD=your-password
NEO4J_DATABASE=your-database-name
GROQ_API_KEY=your-groq-api-key
```

### 2. Database Setup

The notebooks will automatically load a movie dataset from a public CSV source. This includes:
- Movies with ratings and release dates
- Actors and their filmography
- Directors and their films
- Genres

## Usage

### Running the Experiments Notebook

```bash
jupyter notebook experiments.ipynb
```

This notebook demonstrates:
- Connecting to Neo4j
- Loading the movie dataset
- Creating QA chains
- Running various queries

### Running the Prompt Strategies Notebook

```bash
jupyter notebook promptstatergies.ipynb
```

This notebook showcases:
- Few-shot prompt templates
- Custom Cypher prompt engineering
- Improved query generation

## Example Queries

```python
# Initialize the chain (see notebooks for full setup)
chain.invoke("Which actors played in the movie Casino?")
# Output: Robert De Niro, Joe Pesci, Sharon Stone, James Woods

chain.invoke("How many movies has Tom Hanks acted in?")
# Output: 2

chain.invoke("Who was the director of the movie Casino?")
# Output: Martin Scorsese
```

## Project Structure

```
GraphLangchain/
├── experiments.ipynb           # Basic QA chain demonstrations
├── promptstatergies.ipynb      # Advanced prompt engineering
├── requirements.txt            # Python dependencies
├── .gitignore                  # Git ignore rules (protects API keys)
└── README.md                   # This file
```

## Key Components

### Neo4j Graph Database
- Stores movie data with relationships (ACTED_IN, DIRECTED, IN_GENRE)
- Schema includes: Movie, Person, Genre, Actor nodes

### LangChain Integration
- `GraphCypherQAChain`: Main chain for Q&A
- `FewShotPromptTemplate`: Improves query generation with examples
- `ChatGroq`: LLM for understanding and generating responses

### Cypher Query Generation
The system generates Cypher queries like:
```cypher
MATCH (m:Movie {title: 'Casino'})<-[:ACTED_IN]-(a) RETURN a.name
```

## Environment Variables

⚠️ **Security**: Never commit `.env` file or API keys. They are protected by `.gitignore`.

Required variables:
- `NEO4J_URI`: Connection string for Neo4j
- `NEO4J_USERNAME`: Database username
- `NEO4J_PASSWORD`: Database password
- `NEO4J_DATABASE`: Database name
- `GROQ_API_KEY`: API key for Groq LLM

## Troubleshooting

### Connection Issues
- Verify Neo4j is running and accessible
- Check credentials in `.env` file
- Ensure firewall allows connections

### Query Generation Problems
- Check if the graph schema is loaded (`graph.refresh_schema()`)
- Verify example queries in few-shot templates are valid Cypher
- Review generated Cypher in verbose output

### API Key Issues
- Confirm `GROQ_API_KEY` is set in `.env`
- Check API key is valid and has available quota

## Dependencies

- **langchain**: LLM orchestration framework
- **langchain-community**: Community integrations (Neo4j)
- **langchain-groq**: Groq LLM integration
- **neo4j**: Neo4j Python driver
- **python-dotenv**: Environment variable management

## License

Open source - feel free to use and modify for your projects.

## Contributing

Suggestions and improvements welcome! Feel free to submit issues or pull requests.
