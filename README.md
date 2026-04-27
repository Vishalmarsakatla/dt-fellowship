# DT Fellowship — Daily Reflection Tree

## Structure

```
/tree/
  reflection-tree.json     ← Full tree data (40+ nodes, 3 axes)
/agent/
  index.html               ← Working web agent (zero dependencies, no LLM at runtime)
/transcripts/
  persona-1-victor-transcript.md
  persona-2-victim-transcript.md
write-up.md                ← Design rationale (2 pages)
README.md
```

---

## How to Run the Agent

Open `agent/index.html` in any browser. No server required. No npm install. No API keys.

The tree data is embedded directly in the HTML. The engine (~150 lines of vanilla JS) loads it, walks it, and produces the full deterministic conversation.

---

## How to Read the Tree

`tree/reflection-tree.json` contains every node. Key fields:

| Field | Purpose |
|---|---|
| `id` | Unique node identifier |
| `parentId` | Structural parent (for hierarchy) |
| `type` | `start`, `question`, `decision`, `reflection`, `bridge`, `summary`, `end` |
| `text` | What the employee sees. `{A1_OPEN.answer}` interpolates earlier answers. |
| `options` | For questions: fixed choices. For decisions: routing rules. |
| `target` | Explicit jump target (overrides children). |
| `signal` | State tally: `axis1:internal`, `axis2:contribution`, etc. |

**Decision node routing syntax:**
```
"answer=Stormy:A1_Q_HARD"             → if previous answer was X, go to Y
"parent=A1_Q_HARD,answer=...:TARGET"  → if previous node was X AND answer was Y, go to Z
```

**Interpolation syntax in text:**
```
{A1_OPEN.answer}      → employee's answer to node A1_OPEN
{axis1.dominant}      → whichever pole has more tallies on axis 1
{summary_reflection}  → looked up from summary_templates by 3-axis key
```

---

## Node Count

| Type | Count |
|---|---|
| start | 1 |
| question | 11 |
| decision | 5 |
| reflection | 16 |
| bridge | 2 |
| summary | 1 |
| end | 1 |
| **Total** | **37** |

---

## The Three Axes

**Axis 1 — Locus (Victim vs Victor)**  
Grounded in Rotter's Locus of Control (1954) and Dweck's Growth Mindset (2006). Questions surface where the employee expects control to live — through instinct patterns, not self-report.

**Axis 2 — Orientation (Contribution vs Entitlement)**  
Grounded in Campbell et al.'s Psychological Entitlement (2004) and Organ's OCB framework (1988). Separates legitimate recognition needs from entitlement without shaming either.

**Axis 3 — Radius (Self-Centric vs Altrocentric)**  
Grounded in Maslow's Self-Transcendence (1969) and Batson's Perspective-Taking (2011). Maps the employee's radius of concern from narrow (self) to wide (end user).

---

## Design Constraints Honored

- **No LLM at runtime.** The agent makes zero API calls. All text is pre-written, all branching is lookup-based.
- **Deterministic.** Same answers → same path → same reflections. Every time.
- **Fixed options only.** No free-text input.
- **No moralizing.** Every reflection on the "victim/entitlement/self" path names the dynamic, holds it with care, and offers a forward reframe — not a grade.
