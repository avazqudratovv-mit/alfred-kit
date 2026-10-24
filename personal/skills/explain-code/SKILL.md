---
name: explain-code
description: Teach me a file, function or flow line by line, at beginner level, with questions at the end.
argument-hint: [file, function or flow]
disable-model-invocation: true
---

Explain: $ARGUMENTS

1. One paragraph: what this code is for and where it sits in the app.
2. Walk through it in small chunks (5–15 lines). For each chunk: the code, then plain-English explanation. Explain every new term, library function or pattern the first time it appears.
3. Show one example with real values going through it.
4. Point out why it's written this way (design choice) and one thing that could go wrong.
5. One sentence I could say about this code in an interview.
6. End with 3 questions to check I understood. Don't change any code.
