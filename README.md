
# Voice AI Agent 🎙️🤖

A Python-based conversational voice AI agent that listens to user speech, converts it into text, processes the query using OpenAI language models, and responds back using AI-generated speech.

This project demonstrates a complete voice interaction pipeline:

- User Voice → Speech-to-Text → LLM Reasoning → Tool Calling → Text-to-Speech → Voice Response


---

## ✨ Features

* 🎤 **Voice Input**

  * Captures user speech through the microphone.
  * Uses `SpeechRecognition` for speech-to-text conversion.

* 🧠 **Conversational AI**

  * Uses OpenAI chat models to generate intelligent responses.
  * Maintains message history for contextual conversations.

* 🔊 **Text-to-Speech Output**

  * Converts AI responses into natural-sounding speech.
  * Uses OpenAI TTS with streaming audio playback.

* 🛠️ **Tool Calling Support**

  * Can call custom tools based on user intent.
  * Includes examples like:

    * Weather lookup
    * Running system commands

* 🌦️ **Weather Tool**

  * Fetches current weather using `wttr.in`.

* ⚙️ **Command Execution Tool**

  * Supports running local system commands through the AI agent.

---

## 🧠 How It Works

The project contains two main implementations:

### `main.py`

A simple voice conversational agent.

Flow:

```text
User speaks
↓
Speech is converted to text
↓
Text is sent to OpenAI chat model
↓
AI generates response
↓
Response is converted to speech
↓
Audio is played back to user
```

### `cursor.py`

An advanced voice agent with reasoning and tool-calling support.

It follows a structured reasoning flow:

```text
START → PLAN → TOOL → OBSERVE → OUTPUT
```

This allows the agent to decide whether it needs to answer directly or use an external tool first.

---

## 🛠️ Tech Stack

| Component             | Technology              |
| --------------------- | ----------------------- |
| Language              | Python                  |
| Speech-to-Text        | SpeechRecognition       |
| LLM                   | OpenAI GPT models       |
| Text-to-Speech        | OpenAI TTS              |
| Tool Calling          | Custom Python functions |
| Environment Variables | python-dotenv           |
| Weather API           | wttr.in                 |
| Validation            | Pydantic                |

---

## 📁 Project Structure

```text
Voice-AI-agent/
└── Agent/
    └── VoiceAgent/
        ├── main.py
        ├── cursor.py
        └── requirements.txt
```

---

## ⚙️ Installation

### 1. Clone the repository

```bash
git clone https://github.com/pranjalisr/Voice-AI-agent.git
cd Voice-AI-agent/Agent/VoiceAgent
```

### 2. Create a virtual environment

```bash
python -m venv venv
```

Activate it:

```bash
# Windows
venv\Scripts\activate
```

```bash
# macOS/Linux
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

---

## 🔐 Environment Variables

Create a `.env` file inside:

```text
Agent/VoiceAgent/
```

Add your OpenAI API key:

```env
OPENAI_API_KEY=your_openai_api_key_here
```

---

## ▶️ Usage

### Run the basic voice agent

```bash
python main.py
```

### Run the tool-calling voice agent

```bash
python cursor.py
```

Then speak into your microphone when prompted:

```text
Speak Something...
```

Example queries:

```text
What is the weather in Delhi?
```

```text
Tell me a joke.
```

```text
Open calculator.
```

---

## 🧩 Available Tools

### 1. Weather Tool

```python
get_weather(city: str)
```

Fetches current weather for a city.

Example:

```text
What is the weather in Mumbai?
```

### 2. Command Tool

```python
run_command(cmd: str)
```

Runs a system command on the local machine.

Example:

```text
Create a folder named demo
```

> ⚠️ Be careful with command execution. Do not run unsafe or destructive commands.

---

## 🗣️ Voice Output

The agent uses OpenAI’s text-to-speech model with the `coral` voice.

Current TTS model:

```python
gpt-4o-mini-tts
```

The response is streamed and played locally using:

```python
LocalAudioPlayer
```

---

## 🔄 Agent Reasoning Flow

The advanced agent in `cursor.py` uses a structured JSON-based reasoning format:

```json
{
  "step": "PLAN",
  "content": "The user is asking for the weather, so I should use the weather tool."
}
```

Tool call format:

```json
{
  "step": "TOOL",
  "tool": "get_weather",
  "input": "Delhi"
}
```

Final output format:

```json
{
  "step": "OUTPUT",
  "content": "The weather in Delhi is partly cloudy with a temperature of 30°C."
}
```

---

## ✅ Example Workflow

```text
User: What is the weather in Delhi?

Agent Plan:
The user wants weather information.

Tool Call:
get_weather("Delhi")

Observation:
Weather in Delhi is Partly cloudy +30°C

Final Voice Response:
The current weather in Delhi is partly cloudy and around 30°C.
```



---

## ⚠️ Notes

* A working microphone is required.
* Internet connection is required for OpenAI and Google speech recognition.
* Keep your `.env` file private.
* Never commit API keys to GitHub.

---

## 📄 License

This project is open-source and available under the MIT License.

