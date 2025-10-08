# HealthBot: AI-Powered Patient Education System

An AI-powered chatbot that provides personalized, on-demand health information to patients. Built with LangGraph, OpenAI, and Tavily search.

## Project Overview

HealthBot is a healthcare education assistant designed to help patients understand medical conditions, treatment options, and health information in a clear, accessible way. The bot searches for reliable medical information, summarizes it in patient-friendly language, and tests comprehension through interactive quizzes.

## Features

- **Interactive Health Education**: Ask about any health topic or medical condition
- **Real-time Information Retrieval**: Uses Tavily search to find current, reliable medical information
- **Patient-Friendly Summaries**: Converts complex medical information into 3-4 paragraph summaries
- **Comprehension Testing**: Generates quiz questions based on the provided information
- **Intelligent Grading**: Evaluates answers with detailed feedback and citations
- **Continuous Learning**: Option to learn about multiple topics in one session
- **Privacy-Focused**: State resets between topics to maintain patient privacy

## Installation

1. Clone the repository
2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Create a `config.env` file in the project root with your API keys:

**For Vocareum environment:**
```
OPENAI_API_KEY="voc-your-vocareum-key-here"
TAVILY_API_KEY="your-tavily-api-key"
```

**For standard OpenAI:**
```
OPENAI_API_KEY="sk-your-openai-key-here"
TAVILY_API_KEY="your-tavily-api-key"
```

**Note:** The code is configured to work with the Vocareum OpenAI proxy (`https://openai.vocareum.com/v1`). If you're using the standard OpenAI API, update the `base_url` parameter in the notebook to `https://api.openai.com/v1` or remove it to use the default.

## Usage

1. Open the Jupyter notebook:
```bash
jupyter notebook student-starter.ipynb
```

2. Run all cells to start the HealthBot
3. Follow the interactive prompts to:
   - Enter a health topic you want to learn about
   - Read the generated summary
   - Take the comprehension quiz
   - Review your grade and feedback
   - Choose to learn about another topic or exit

## Architecture

### State Management
The HealthBot uses a comprehensive state class that tracks:
- User's selected topic
- Search results from Tavily
- Generated summary
- Quiz question and user's answer
- Grade and explanation
- Session continuation choice

### Workflow Nodes
1. **collect_topic**: Asks patient what they want to learn about
2. **search_topic**: Uses Tavily to find medical information
3. **summarize_results**: Creates patient-friendly summary using GPT-4
4. **display_summary**: Shows summary and waits for user
5. **generate_quiz**: Creates a quiz question based on summary
6. **collect_answer**: Gets patient's answer
7. **grade_answer**: Evaluates answer with detailed feedback
8. **display_grade_and_ask_continue**: Shows results and asks to continue
9. **reset_for_new_topic**: Resets state for new learning session
10. **end_session**: Exits the application

### Conditional Routing
The workflow includes intelligent routing that allows users to:
- Learn about another topic (loops back to collect_topic)
- Exit the session (ends the workflow)

## Requirements Met

### Model and Tools Configuration ✅
- OpenAI and Tavily API keys properly configured
- Successful API calls to both services
- OpenAI successfully calls Tavily for search

### Summarization ✅
- Model calls Tavily for health topics
- Receives and processes search results
- Well-written prompt ensures summarization uses only Tavily data
- Creates 3-4 paragraph patient-friendly summaries

### Quiz Generation and Grading ✅
- Model creates quiz questions using only summary data
- Questions are answerable from summary alone
- Model grades answers using only the summary
- Provides letter grade (A, B, C, D, F) with detailed justification
- Includes citations from summary to reinforce learning

### State Management ✅
- Comprehensive state class with all necessary properties
- State is updated appropriately by each node
- Subsequent nodes can access previous state data
- Messages history maintained for model context

### Nodes, Edges, and Workflow ✅
- Multiple nodes with single responsibilities
- Nodes properly reference and update state
- Sequential edge configuration for workflow
- Conditional edges for restart/exit logic
- Complete workflow allows users to: enter topic, see summary, take quiz, see grade, restart or exit

## Technologies Used

- **LangGraph 0.2.50**: Workflow orchestration and state management
- **LangChain 0.3.25**: LLM integration and tooling framework
- **LangChain-OpenAI 0.3.33**: OpenAI integration with enhanced features
- **OpenAI GPT-4**: Language model for summarization, quiz generation, and grading (via Vocareum proxy)
- **Tavily 0.5.0**: Real-time web search for medical information
- **HTTPX 0.28.1**: HTTP client for secure API communications
- **Python 3.10+**: Core programming language

## Future Enhancements

- Difficulty settings (beginner, intermediate, advanced)
- Multiple quiz questions per topic
- Related topic suggestions
- Session history and progress tracking
- Multi-language support
- Voice interface option

## License

See LICENSE file for details.

## Troubleshooting

### SSL Certificate Errors

If you encounter SSL certificate verification errors when connecting to the Vocareum OpenAI proxy, the code includes built-in workarounds:

1. **SSL Context Workaround**: The notebook automatically configures Python's SSL context to handle Vocareum's certificates
2. **HTTPX Client Configuration**: An HTTPX client with SSL verification disabled is used for API calls to the Vocareum proxy

These workarounds are safe for the Vocareum educational environment but should be reviewed if deploying to production.

### API Connection Issues

- **Vocareum Users**: Ensure your API key starts with `voc-` and is valid
- **Standard OpenAI Users**: Update the `base_url` in the notebook to `https://api.openai.com/v1` or set it to `None`
- **Rate Limiting**: If you encounter rate limits, wait a few minutes before retrying

### Package Version Conflicts

If you experience version conflicts:
```bash
pip install -r requirements.txt --upgrade --force-reinstall
```

## Disclaimer

This is an educational tool and should not replace professional medical advice. Always consult healthcare professionals for medical concerns.

