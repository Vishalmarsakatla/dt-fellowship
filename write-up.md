# Write-Up: Design Rationale for the Daily Reflection Tree

## Why These Questions

The hardest constraint in this assignment is the ban on free text. When you strip away open-ended input, you lose the ability to meet the employee exactly where they are — which means the questions themselves have to do more lifting. Every option had to be written so that a real person arriving tired at 7pm would find *their* answer in the list, not a near-miss they settle for.

This pushed me toward **phenomenological language**: weather reports, driving vs. drifting, the "frame" of a challenge. These aren't corporate abstractions. They're the way people actually talk about their days when they're not being formal. The opening question ("If today were a weather report...") sets that register immediately — it signals that this is a reflection, not a performance review.

The psychological anchors for each axis came directly from the source literature:

**Axis 1 (Locus):** Rotter's original construct is about expectancies — where do you *expect* control to live? The questions surface this through response patterns rather than self-report. Asking "what was your first instinct?" is more honest than "do you feel in control?" because instincts are harder to perform for. Dweck's growth mindset framing comes in through the follow-ups — the difference between "I got lucky" and "I adapted fast" captures whether the employee attributes outcomes to fixed circumstances or to their own responsiveness.

**Axis 2 (Orientation):** The entitlement literature (Campbell et al.) is careful to separate *entitlement* from *legitimate need for feedback*. A person wanting recognition isn't necessarily entitled — they might just need to know their work landed. I designed the entitlement-path reflections to hold this distinction carefully. The reflection `A2_R_ENT_GENTLE` explicitly offers the employee an alternative reading: "Is this about deserving, or about knowing you made a difference?" This respects the psychology without letting the employee off the hook. Organ's OCB framework informed the contribution questions — specifically the emphasis on *discretionary* effort, things done beyond role requirements.

**Axis 3 (Radius):** Maslow's 1969 paper on self-transcendence is often skipped in pop psychology summaries of his hierarchy. The core idea is that the highest human motivation isn't self-actualization but *contribution to something larger than the self*. The four options in `A3_OPEN` are deliberately ordered from narrowest to widest radius — not random. Batson's perspective-taking work informed the dyadic questions: frustration with a colleague is still a form of other-awareness, and the reflection for that path uses it as an opening rather than a criticism.

---

## How the Branching Works

The tree has two levels of branching per axis: a **routing decision** (based on the opening answer) and a **nuance decision** (based on the follow-up). This creates 4-5 possible paths per axis, not just two.

The key trade-off I made was **depth over breadth on Axis 1**. Axis 1 has the most elaborate branching because it's the foundational axis — the employee's relationship to agency colors everything that follows. Someone arriving on `A1_R_EXT_STRONG` needs a different entry into Axis 2 than someone on `A1_R_INT_STRONG`. I use the bridge nodes to do that reorientation: `BRIDGE_1_2` is deliberately simple ("From how you handled things — to what you gave") because the employee is already carrying the Axis 1 insight and doesn't need another reframe yet.

The signal tallying system keeps the summary honest. If an employee ends up on three contribution/internal/altrocentric reflections, the summary template reads very differently than the external/entitlement/self combination. The summary templates are named tuples of the dominant signals — eight combinations covering the full state space, each written as a specific, non-generic closing thought.

The interpolation system (`{A1_OPEN.answer}`) makes the summary feel personal without any LLM involvement. "Today you called it 'Stormy'" lands differently than "Based on your responses..." — it mirrors the employee's own words back at them, which is a known technique in reflective practice.

---

## What I'd Improve With More Time

**1. The entitlement axis needs a third path.** Right now, `A2_OPEN` routes employees either into contribution or entitlement based on their opening answer. A real employee might be genuinely unsure — they gave a lot and *also* felt unrecognized, and the two feelings coexist. A "both" option in the opening question would surface that complexity, with a distinct path that holds the tension rather than resolving it.

**2. Axis 3 needs a time dimension.** Self-transcendence isn't a stable trait — it fluctuates hour to hour. A question like "Compare your concern radius at 9am versus now" would capture whether the employee *narrowed* over the course of a day (a warning sign of depletion) or *widened* (a sign of growth). The current structure captures a snapshot, not a trajectory.

**3. The summary templates are eight-point, but the tree can produce finer-grained states.** With more time, I'd parameterize the summary further — not just by dominant signal per axis, but by *margin*. Someone who consistently chose internal/contribution/altrocentric options needs a different closing than someone who barely tipped that way on two axes and went the other direction on the third.

**4. Session history.** The most powerful reflection tool would hold a thirty-day view — not individual sessions but drift patterns. Are you consistently external on Axis 1 on Mondays? Does your radius narrow at the end of quarters? None of that requires LLM inference; it requires storing signals over time and surfacing them as context at the start of each session.
