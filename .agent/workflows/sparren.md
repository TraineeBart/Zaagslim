---
description: Brainstorm and discuss ideas without building anything
---

# Workflow: Sparring Session

Use this workflow for brainstorming, architecture discussions, trade-off analysis, and strategic planning. **No code is written. No files are changed (except context docs).**

## Phase 1: Context Loading

// turbo
1. Read current state:
```bash
cd /Users/bb2-1/Documents/Zaagslim && head -60 .context/STATUS.md && echo "---" && cat .context/STRATEGIC_NOTES.md
```

2. Read relevant context based on the topic:
   - Architecture → `.context/DECISIONS.md`
   - Roadmap → `.context/STATUS.md` (Roadmap + Backlog sections)
   - Strategy → `.context/STRATEGIC_NOTES.md`
   - Codebase → `.context/CODEBASE_MAP.md`

3. Acknowledge: *"Context geladen. Huidige fase: [X]. Onderwerp: [Y]."*

## Phase 2: Discussion

4. **Listen first** — let the user explain what they want to discuss.

5. **Structure the conversation**:
   - Present options with trade-offs (never just one answer)
   - Use concrete examples from the codebase
   - Challenge assumptions: "Maar wat als...?"
   - Keep scope visible: "Dit raakt aan [X], wil je dat nu bespreken of parkeren?"

6. **Prevent scope creep into building**:
   - If the user says "laten we dat maar meteen doen" → STOP
   - Respond: *"Dat klinkt als een /new-feature sessie. Zullen we dit als volgende sessie inplannen?"*

## Phase 3: Capture

7. **Log outcomes** (only if actionable decisions were made):
   - Strategic insights → update `.context/STRATEGIC_NOTES.md`
   - Architecture decisions → update `.context/DECISIONS.md`
   - New work items → add to STATUS.md backlog

8. **Session handover**:
   - Schrijf een korte handover (zie Handover Format hieronder)
   - Presenteer aan de user

## Handover Format

```
📋 Sessie: [onderwerp]
🧠 Key insight: [1 zin]
📌 Actiepunten: [lijst, of "geen — puur sparren"]
🔜 Volgende sessie: [suggestie]
```

## Rules

- ❌ Geen code schrijven
- ❌ Geen bestanden aanmaken (behalve context docs)
- ❌ Geen tests draaien
- ✅ Wel: diagrammen tekenen, opties uitwerken, risico's benoemen
- ✅ Wel: vragen stellen die de user aan het denken zetten
