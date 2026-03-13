Personal AI Agent
A minimal AI chatbot in a single HTML file
HTML · JavaScript · AI API

About
This is a personal AI agent I built using nothing but plain HTML and vanilla JavaScript. There is no framework, no CSS library, no backend server, and no build process. A single .html file is all you need — open it in any browser and start chatting.
I built this to understand how AI apps work at their most fundamental level. Every major chatbot product uses the same core pattern — this project strips away all the layers and shows exactly what is happening under the hood.

Features

AI-powered replies using a state-of-the-art language model
Full conversation memory — the agent remembers everything said in the session
Next steps suggestions — the agent always ends with actionable follow-ups
Enter to send, Shift+Enter for a new line
Error handling — clear messages if something goes wrong
Zero dependencies — no npm, no build tools, no install needed


How to Run

Download or clone this repository
Open agent.html in VS Code
Double-click the file to open in your browser
Paste your API key in the input box at the top
Start chatting


How It Works
1. The HTML Structure
Three elements make up the entire UI:
<div id="chat">          — scrollable conversation window
<textarea id="input">    — where you type
<button onclick="send()"> — triggers the AI call
2. The System Prompt
I control the agent's personality with a single string sent on every request:
javascriptconst SYSTEM = `You are a helpful personal agent. Be clear and concise.
Always end with a "Next steps:" section listing 1-3 suggestions.`
Change this one string and the entire behaviour of the agent changes instantly.
3. Conversation Memory
The AI has no built-in memory between calls. I built a history array that stores every message and sends the full conversation each time — this is how every chatbot maintains context:
javascripthistory.push({ role: "user", content: text });       // before call
history.push({ role: "assistant", content: reply });  // after call
4. The API Call
A standard fetch() POST request to the AI endpoint:
javascriptfetch("https://api.anthropic.com/v1/messages", {
  method: "POST",
  headers: { "x-api-key": apiKey, "anthropic-version": "2023-06-01" },
  body: JSON.stringify({ model, max_tokens, system, messages: history })
})
```

---

## Project Structure
```
personal-agent/
│
├── agent.html    ← the entire project (single file)
└── README.md     ← this file

Tech Stack

HTML5 — structure and layout
Vanilla JavaScript — all logic, API calls, DOM updates
AI API — language model powering the responses
fetch() — built-in browser function for HTTP requests


What I Learned

How to call a REST API directly from the browser using fetch()
How async/await works for handling real-time responses
How AI conversation memory works under the hood
How system prompts control AI behaviour
How to build a fully functional AI app with under 60 lines of code


Customisation
To change the agent's behaviour, edit the SYSTEM constant:
javascriptconst SYSTEM = `You are a coding assistant. Only answer programming questions.
Always provide code examples. Keep answers under 5 sentences.`
That one string is all it takes.

Licence
MIT — free to use, modify, and distribute.
