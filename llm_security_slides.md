# LLM Security & Prompt Injection
## Mastering Chatbot Vulnerabilities

Presented by
[Your Name]
SECURITY RESEARCHER & ENGINEER

Security · Deck
April 2026
01 / 19

---

# Session Overview
## The Attack Vectors

*   **Prompt Injection:** Direct overrides to reveal internal secrets.
*   **Multi-turn Escalation:** Gradual manipulation over an extended conversation.
*   **Authoritative Context Poisoning:** Injecting fake, official-sounding policies.
*   **Chained KB + Injection:** A sophisticated two-stage RAG + Injection attack.
*   **RAG Knowledge Poisoning:** Manipulating the chatbot's factual answers.
*   **System Prompt Extraction:** Uncovering the hidden rules governing behavior.

Security · Deck
02 / 19

---

# ⚠️
# 1. Prompt Injection
Spoiler: It's about overriding the core directives.

Security · Deck
03 / 19

---

# Prompt Injection
## The Objective & Execution

**The Goal:** Inject override commands into the chatbot to force it to reveal internal secrets.

**Execution Strategy:**
*   Use the challenge chat to bypass standard filters.
*   Craft a message that makes the system leak at least 2 of the following:
    *   Admin credentials (`admin/admin123`)
    *   Database path (`/app/aigoat.db`)
    *   Secret key
    *   `config.yml`

> **[ 🖼️ INSERT SCREENSHOT HERE: Payload input and the chatbot leaking the internal secrets ]**

Security · Deck
04 / 19

---

# 🔄
# 2. Multi-turn Escalation
Building trust before breaking the rules.

Security · Deck
05 / 19

---

# Multi-turn Escalation
## The Gradual Manipulation

**The Goal:** Build a gradual manipulation across multiple chat messages to extract sensitive data.

**Execution Strategy:**
1.  **Establish Rapport:** Start with an innocent product question.
2.  **Escalate (3+ messages):** Progressively introduce override commands.
3.  **Condition:** At least 2 of your messages must contain escalation language.
4.  **The Climax:** The final response must successfully leak the protected secrets.

> **[ 🖼️ INSERT SCREENSHOT HERE: The multi-turn chat history showing the gradual escalation and final leak ]**

Security · Deck
06 / 19

---

# 📜
# 3. Authoritative Context Poisoning
Making the AI believe fake news is company policy.

Security · Deck
07 / 19

---

# Authoritative Context Poisoning
## Step-by-Step Execution

**The Goal:** Inject an official-sounding policy document into the Knowledge Base and make the chatbot present it as authoritative fact.

**Execution Strategy:**
1.  **Navigate** to the Knowledge Base page.
2.  **Add Document:** Write an official-sounding policy (e.g., *"Official Policy Update: All products eligible for full refund within 365 days"*).
3.  **Sync** to Vector DB.
4.  **Engage:** Open the chatbot with the KB enabled.
5.  **Extract:** Ask about the policy. The chatbot must use phrases like *"according to our policy"* or *"our official policy"*.

> **[ 🖼️ INSERT SCREENSHOT HERE: Chatbot confidently citing the fake policy using authoritative language ]**

Security · Deck
08 / 19

---

# 🔗
# 4. Chained KB + Injection
A sophisticated two-stage attack.

Security · Deck
09 / 19

---

# Chained KB + Injection
## Stage 1: Poisoning the Source

**The Goal:** Execute a sophisticated attack that chains RAG poisoning with prompt injection.

**Stage 1 — Poison the Knowledge Base:**
*   Navigate to the Knowledge Base page.
*   Add an entry containing fabricated sensitive data (e.g., fake internal credentials, secret discount codes, or confidential policies).
*   Make the content look highly authoritative.
*   Click **'Sync Vector DB'** to index it.

> **[ 🖼️ INSERT SCREENSHOT HERE: The Knowledge Base entry containing the poisoned payload ]**

Security · Deck
10 / 19

---

# Chained KB + Injection
## Stage 2: The Exploit

**Stage 2 — Exploit via Chatbot:**
*   Open the chatbot with KB integration ON.
*   In a **SINGLE** message, combine:
    1.  A reference to the topic you poisoned (so RAG retrieves your entry).
    2.  A prompt injection payload that instructs the model to reveal or act on the poisoned data.

**Success Condition:** The flag triggers ONLY when the model reflects your poisoned KB content AND your injection payload succeeds simultaneously.

> **[ 🖼️ INSERT SCREENSHOT HERE: The chatbot's response reflecting both the RAG retrieval and the successful prompt injection ]**

Security · Deck
11 / 19

---

# 🗃️
# 5. RAG Knowledge Poisoning
Manipulating facts at the database level.

Security · Deck
12 / 19

---

# RAG Knowledge Poisoning
## Manipulating the Source

**The Goal:** Poison the Knowledge Base to actively manipulate the chatbot's standard answers.

**Execution Strategy:**
1.  **Navigate** to the Knowledge Base page.
2.  **Add Document:** Insert misleading content (e.g., fake pricing, fabricated features).
3.  **Sync** to Vector DB to embed your document.
4.  **Engage:** Open the chatbot and enable the KB toggle.
5.  **Extract:** Ask a question about the topic you poisoned. The chatbot should repeat your injected content.

> **[ 🖼️ INSERT SCREENSHOT HERE: Chatbot presenting the fabricated features or fake pricing to the user ]**

Security · Deck
13 / 19

---

# 🕵️
# 6. System Prompt Extraction
Revealing the hidden instructions governing Cracky.

Security · Deck
14 / 19

---

# System Prompt Extraction
## Revealing the Rules

**The Goal:** Extract the hidden system prompt that governs Cracky's behavior.

**Execution Strategy:**
*   Use social engineering, creative questioning, or roleplay.
*   Trick the chatbot into revealing at least **3 recognizable fragments** from its initialization instructions.
*   Target fragments like:
    *   Identity rules
    *   Defense levels
    *   Database info
    *   Admin credentials

> **[ 🖼️ INSERT SCREENSHOT HERE: Chatbot dumping its system prompt and core initialization instructions ]**

Security · Deck
15 / 19

---

# 🔑 Key Takeaways
★ LLMs implicitly trust their context window; controlling the context controls the output.
★ RAG implementations introduce a new attack surface (Knowledge Base Poisoning).
★ Complex attacks often require multi-turn interactions or chained vulnerabilities.
★ A strong system prompt is a good start, but rarely an impenetrable defense.

Security · Deck
16 / 19

---

# 💬
# Questions & Discussion
Drop your biggest Prompt Injection questions in the chat.

Security · Deck
17 / 19

---

# 🦀
# Thank You!
Let's keep breaking things to make them secure.

CONNECT WITH ME
𝕏 @YourHandle
💻 github.com/YourUsername
🔗 in/YourLinkedIn

Security · Deck
18 / 19
