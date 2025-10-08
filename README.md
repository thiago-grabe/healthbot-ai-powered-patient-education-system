# 🏥 HealthBot: AI-Powered Patient Education System

<div align="center">

An intelligent, interactive healthcare education assistant that makes learning about medical conditions accessible and engaging.

**Built with LangGraph • OpenAI GPT-4 • Tavily Search**

[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![LangChain](https://img.shields.io/badge/LangChain-0.3.25-green.svg)](https://python.langchain.com/)
[![LangGraph](https://img.shields.io/badge/LangGraph-0.2.50-orange.svg)](https://langchain-ai.github.io/langgraph/)

</div>

## 📖 Project Overview

HealthBot is a sophisticated healthcare education assistant designed to bridge the gap between complex medical information and patient understanding. Using state-of-the-art AI and real-time web search, it delivers:

- **Clear, Evidence-Based Information**: Searches trusted medical sources in real-time
- **Patient-Friendly Language**: Transforms complex medical jargon into understandable explanations
- **Interactive Learning**: Tests comprehension with AI-generated quizzes
- **Personalized Feedback**: Provides detailed, encouraging feedback with citations
- **Beautiful UI**: Professional, emoji-enhanced interface with step-by-step guidance

## ✨ Features

### Core Functionality
- 🔍 **Smart Health Search**: Real-time medical information retrieval via Tavily API
- 📚 **AI Summarization**: GPT-4 creates patient-friendly 3-4 paragraph summaries
- 🎯 **Custom Quizzes**: Automatically generated comprehension checks
- 📊 **Intelligent Grading**: Detailed feedback with citations from the summary
- 🔄 **Multi-Topic Learning**: Learn about multiple conditions in one session
- 🔐 **Privacy-First**: State resets between topics for data protection

### Enhanced User Experience
- 🎨 **Beautiful Interface**: Professional formatting with emojis and clear sections
- 📍 **Progress Tracking**: Step indicators (1/4, 2/4, etc.) show your progress
- 💬 **Interactive Prompts**: Contextual icons and formatted input requests
- ✅ **Status Messages**: Real-time feedback on search, analysis, and processing
- 🌟 **Encouraging Feedback**: Grade-based congratulations and improvement tips
- 📋 **Clear Instructions**: Detailed guidance at every step

### Technical Excellence
- 🔧 **Robust Error Handling**: Graceful fallbacks for API or search issues
- 🔍 **Debug Mode**: Built-in test cell for troubleshooting Tavily searches
- 🔒 **SSL Support**: Automatic handling for Vocareum proxy environments
- ⚡ **Optimized Performance**: Efficient state management with LangGraph
- 📝 **Comprehensive Logging**: Informative messages for better debugging

## 🚀 Quick Start

### Prerequisites
- Python 3.10 or higher
- pip (Python package manager)
- Jupyter Notebook or JupyterLab

### Installation Steps

1. **Clone the repository**
```bash
git clone <repository-url>
cd healthbot-ai-powered-patient-education-system
```

2. **Install dependencies**
```bash
pip install -r requirements.txt
```

3. **Set up API keys**

Create a `config.env` file in the project root:

**For Vocareum Environment:**
```env
OPENAI_API_KEY="voc-your-vocareum-key-here"
TAVILY_API_KEY="tvly-your-tavily-key-here"
```

**For Standard OpenAI:**
```env
OPENAI_API_KEY="sk-your-openai-key-here"
TAVILY_API_KEY="tvly-your-tavily-key-here"
```

4. **Get your API keys**
   - **Vocareum OpenAI**: Provided by your course/institution
   - **Tavily API**: Free tier at [tavily.com](https://tavily.com/) (sign up takes 2 minutes)

### Configuration Notes

- ✅ Default: Configured for Vocareum OpenAI proxy (`https://openai.vocareum.com/v1`)
- 🔄 Standard OpenAI: Update `base_url` in Cell 2 to `https://api.openai.com/v1`
- 🔐 Security: Never commit `config.env` to version control (included in `.gitignore`)

## 💡 Usage Guide

### Starting HealthBot

1. **Launch Jupyter Notebook**
```bash
jupyter notebook student-starter.ipynb
```

2. **Run the cells in order:**
   - **Cell 0**: Read the setup instructions (Markdown)
   - **Cell 1**: Load and verify API keys
   - **Cell 2**: Initialize HealthBot and start the session
   - **Cell 3** (Optional): Test Tavily search if you encounter issues

### Interactive Workflow

The HealthBot guides you through a 4-step learning process:

#### 🔹 Step 1: Choose Your Topic
```
🔍 What health topic or medical condition would you like to learn about?
   ➤ diabetes
```
Enter any medical condition, symptom, or health topic. Be specific for better results!

#### 🔹 Step 2: Review the Summary
The AI searches medical sources and creates a patient-friendly summary. Take your time reading!

#### 🔹 Step 3: Take the Quiz
Answer a multiple-choice question to test your understanding.
```
❓ Question: What is the primary function of insulin?
   A) To break down proteins
   B) To regulate blood sugar levels
   C) To produce red blood cells
   D) To filter waste from blood

✍️ Your answer: B
```

#### 🔹 Step 4: Get Feedback
Receive your grade with detailed explanations and citations from the summary.

### Example Session
```
═══════════════════════════════════════════════════════════════
🏥  WELCOME TO HEALTHBOT
═══════════════════════════════════════════════════════════════

🔹 Step 1/4: Searching for reliable medical information...
✅ Found 3 reliable sources! Preparing your summary...

🔹 Step 2/4: Creating your personalized health summary...

📚 Health Information Summary: Diabetes
──────────────────────────────────────────────────────────────
    [AI-generated patient-friendly summary appears here]
──────────────────────────────────────────────────────────────

🔹 Step 3/4: Generating a quiz to test your understanding...

🎯 Comprehension Check Quiz
──────────────────────────────────────────────────────────────
    ❓ Question: [Quiz question appears here]
──────────────────────────────────────────────────────────────

🔹 Step 4/4: Evaluating your answer...

🎓 Your Quiz Results
──────────────────────────────────────────────────────────────
   🌟 Your Grade: A

   💬 Detailed Feedback:
       [Personalized feedback with citations]
──────────────────────────────────────────────────────────────

🔄 What would you like to do next?
   [1] 📚 Learn about another health topic
   [2] 🚪 Exit HealthBot
```

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

## 🐛 Troubleshooting

### Common Issues and Solutions

#### ❌ "Search results are garbage/random characters"

**Problem**: Tavily returns unintelligible data  
**Cause**: Invalid or expired Tavily API key  
**Solution**:
1. Visit [tavily.com](https://tavily.com/) and sign in
2. Generate a new API key
3. Update your `config.env` file with the new key
4. Restart the Jupyter kernel: `Kernel → Restart Kernel`
5. Run Cell 3 (Test Cell) to verify the search works

**Quick Test**:
```python
# Uncomment and run Cell 3 to debug
test_results = tavily_tool.invoke({"query": "diabetes symptoms"})
print(test_results)
```

#### ❌ "InvalidUpdateError: Expected node to update at least one state field"

**Problem**: Node returns empty dictionary  
**Cause**: LangGraph requires all nodes to update state  
**Solution**: ✅ Already fixed in the latest version! Just pull/update the code.

#### ❌ "SSL Certificate Verification Failed"

**Problem**: SSL errors when connecting to Vocareum OpenAI proxy  
**Cause**: Vocareum uses custom certificates  
**Solution**: ✅ Automatic! The notebook includes:
- SSL context configuration for Python
- HTTPX client with disabled verification
- Warning suppression for cleaner output

**No manual intervention needed** - just run the code!

#### ❌ "API Connection Error" or "Authentication Failed"

**Problem**: Cannot connect to OpenAI API  
**Cause**: Invalid API key or wrong base URL  
**Solutions**:

**For Vocareum users:**
- Ensure key starts with `voc-`
- Verify key is active in your Vocareum workspace
- Check `config.env` has: `OPENAI_API_KEY="voc-..."`

**For standard OpenAI users:**
- Ensure key starts with `sk-`
- Update Cell 2: Change `base_url` to `"https://api.openai.com/v1"`
- Or set `base_url=None` to use default

#### ❌ "No module named 'langchain'" or Import Errors

**Problem**: Missing dependencies  
**Cause**: Packages not installed  
**Solution**:
```bash
# Install all requirements
pip install -r requirements.txt

# If issues persist, force reinstall
pip install -r requirements.txt --upgrade --force-reinstall
```

#### ❌ "Rate Limit Exceeded"

**Problem**: Too many API requests  
**Cause**: Hit Tavily or OpenAI rate limits  
**Solution**:
- **Tavily**: Free tier has limited searches/day - wait or upgrade
- **OpenAI**: Wait a few minutes between requests
- **Vocareum**: Check your institution's rate limits

### Debug Mode

**Cell 3** includes a test function to debug Tavily searches:

1. Open `student-starter.ipynb`
2. Go to Cell 3
3. Remove the `"""` markers (uncomment the code)
4. Run the cell
5. Inspect the output to see exactly what Tavily returns

This helps identify:
- API key validity
- Result format issues
- Content quality problems

### Getting Help

If issues persist:

1. **Check Cell 1 output**: Verify both API keys loaded correctly
2. **Review error messages**: They often indicate the exact problem
3. **Test independently**: Use Cell 3 to isolate Tavily issues
4. **Restart kernel**: `Kernel → Restart Kernel` clears state issues
5. **Check logs**: Look for warnings or error messages in output

## 💡 Tips for Best Results

### Getting Quality Information

1. **Be Specific**: Instead of "heart problems" try "symptoms of coronary artery disease"
2. **Use Medical Terms**: Common medical terminology often yields better results
3. **One Topic at a Time**: Focus on one condition for comprehensive understanding
4. **Read Carefully**: Take time with the summary before the quiz

### Example Good Topics

✅ "Type 2 diabetes symptoms and management"  
✅ "High blood pressure causes and treatment"  
✅ "Vitamin D deficiency"  
✅ "Migraine headache triggers"  
✅ "Seasonal allergies prevention"  

### Topics to Avoid

❌ Too vague: "health" or "medicine"  
❌ Multiple topics: "diabetes and heart disease"  
❌ Non-medical: "best diet for weight loss"  

## ⚠️ Important Disclaimers

### Medical Advice

**This is an educational tool ONLY and should NOT replace professional medical advice.**

- ✅ **Use for**: Learning about health conditions, understanding medical terms, general health education
- ❌ **Do NOT use for**: Self-diagnosis, treatment decisions, medical emergencies

### When to See a Doctor

**Always consult healthcare professionals if you:**
- Experience new or worsening symptoms
- Need diagnosis or treatment
- Have questions about medications
- Face a medical emergency (call emergency services immediately)

### Data Accuracy

- Information is sourced from web searches and may not be complete
- Medical knowledge evolves - verify with current medical sources
- AI-generated content should be verified by healthcare providers
- This tool does not replace evidence-based medical literature

### Privacy

- Your health queries are processed by third-party APIs (OpenAI, Tavily)
- Session data resets between topics for privacy
- Do not enter personal health information or identifiable data
- For HIPAA-compliant health information, consult official medical systems
