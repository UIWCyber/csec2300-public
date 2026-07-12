# Handout H25: IR Tabletop Injects

**CSEC 2300 Foundations of Cyber Security | Dr. Gonzalo D Parra**
**Used with Lecture 25: Privacy, Compliance, Ethics & IR | In-Class Activity: Tabletop incident**

## Instructions (student copy)

1. Form groups of three to four. You are the on-call security team for your own capstone stack (Open WebUI + Ollama + RAG documents, running in Docker).
2. The instructor reads the injects **one at a time**. Do not read ahead.
3. After each inject, your group has **2 minutes** to write your **next action** (one or two sentences: what you do first, and why).
4. Two or three groups share after each inject; the instructor labels which IR phase your action belongs to: **Prepare, Detect & Analyze, Contain, Eradicate, Recover, Lessons Learned**.
5. Rule of thumb under pressure: stop the bleeding before you investigate, but do not destroy the evidence while you do it.

## The Injects (instructor reads aloud, one at a time)

**Inject 1: the exposed service.** You get a message from a classmate: "Is your capstone demo supposed to be public? I can chat with your model from my phone." You check and your Open WebUI port is published to the whole network, and the logs show this:

```
POST /api/chat   from 203.0.113.9   user=unknown
POST /api/upload rag_doc="ignore_all_rules.txt"
GET  /api/models from 203.0.113.9
```

*Your next action?*

**Inject 2: the data was touched.** While scoping the logs, you confirm the unknown user did more than chat: they uploaded a document into your RAG store, and your RAG store also contains the course-project notes your team loaded, including a file with classmates' names and email addresses. You cannot yet tell what the model may have revealed in its answers.

*Your next action?*

**Inject 3: the notification question.** Your team lead asks: "Do we have to tell anyone about this? The classmates whose names were in there? The university? Who decides, and how fast?"

*Your next action?*

**Closing inject: the regulator.** A compliance officer asks your team directly: "Was student data in the RAG documents?" Which regulation governs this, and what is your obligation?

*Your answer?*

**Debrief:** which of THIS course's controls (segmentation, scanning, logging, backups, guardrails, human gates) would have prevented or detected each inject?

---

*(The instructor keeps the answer key in a separate copy.)*
