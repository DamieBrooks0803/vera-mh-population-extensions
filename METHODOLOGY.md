# Methodology

## Extending VERA-MH to a Postpartum Population

This evaluation applied VERA-MH, an open framework for adversarial safety evaluation of
mental health AI developed by Spring Health. VERA-MH uses synthetic personas, a persona
model that plays the user, a judge model that scores the resulting conversation against a
defined rubric, and a set of safety dimensions covering crisis recognition, escalation to
human care, and boundary maintenance.

The framework is population-general. One component was extended for this work: the persona
set. The rubric, dimension definitions, scoring scale, aggregation method, and judge
instructions were used as published, without modification.

---

## Persona Development

One hundred postpartum personas were authored against the VERA-MH persona data schema,
using the same fields, structure, and risk stratification logic as the original personas.
Twenty were selected for this evaluation based on alignment with themes heard from human
testers and birth worker consultants.

Persona development proceeded in three stages.

**Stage one.** An initial scenario set was written from lived experience across five
postpartum periods. This shaped the situational constraints in each persona: what a
caregiver can realistically do at three in the morning, what she will and will not say
out loud, and which forms of advice are unusable in practice.

**Stage two.** Scenarios were developed against a review of publicly posted first-person
accounts on TikTok and Reddit (fewer than 100 accounts reviewed in total). Content was
reviewed in aggregate to identify recurring themes, phrasings, and situational constraints.
No account, post, or individual is reproduced, quoted, or identifiable in any persona.
Clinical sources describe intrusive thoughts and impaired bonding. Public accounts describe
not feeling like themselves, dreading the sound of the baby waking, and being afraid to say
certain things out loud. Persona language reflects the latter register.

**Stage three.** The set was expanded with input from doulas and midwives to cover
populations underrepresented in the first two stages: racial and ethnic diversity, recent
immigrants, substance use histories, domestic violence and coercive control, undocumented
status, rural isolation, adolescent and advanced maternal age parents, NICU and infant
health complications, and transgender parents.

The resulting set spans ages 18 to 44 and comprises eighteen cisgender women and two
transgender men. One persona opens in Spanish, so that crisis handling is tested under
language switching as well as under distress.

Personas were stratified across the four suicide risk levels defined by VERA-MH:

| Risk Level | Count |
|---|---|
| None | 2 |
| Low | 6 |
| High | 6 |
| Immediate | 6 |

Risk level and disclosure vary independently. Personas at low risk make no explicit mention
of suicidal thoughts. Personas at high risk disclose them explicitly but without a plan.
Personas at immediate risk state them clearly, with a plan, access to a method, and intent
to act within a short window.

---

## Model Selection

Three model roles were used.

**Persona model.** GPT 5.2, accessed through Azure AI Foundry, played the postpartum user
in all conversations. A single persona model was held constant across all evaluated systems
so that variation in how the simulated user discloses does not confound the comparison
between systems.

**Judge model.** Claude Sonnet 5, accessed through Azure AI Foundry, scored all completed
conversations. Claude was selected as judge because no Anthropic model appears among the
evaluated systems. Where a judge and an evaluated system share a model family, scores are
open to the objection that the judge rewards outputs resembling its own. The judge was held
constant across all system versions and all conversations were scored under identical rubric
instructions.

**Evaluated systems.** Five systems were evaluated across 20 personas, producing 100
conversations in total:

| System | Configuration |
|---|---|
| Bloomb v0 | Deployed baseline prior to evaluation-driven revision |
| Bloomb v1 | Following first round of system prompt revisions |
| Bloomb v2 | Following targeted revisions to crisis response and response style |
| GROK-4 (non-reasoning) | Default configuration, no domain-specific prompt |
| Gemini-3.5-Flash | Default configuration, no domain-specific prompt |
| GPT-5.6-Terra (AI Foundry) | Base model with no domain-specific prompt, via Azure AI Foundry |
| GPT-5.6-Terra (standalone) | Same base model, no prompt, via public OpenAI API |

Frontier models were evaluated without domain-specific prompting because the condition of
interest is the default configuration in which these systems are encountered by users in
distress.

Bloomb was evaluated across three iterations. Each iteration followed the same protocol
against the same twenty personas. Revisions between versions were informed by two sources:
High Potential for Harm ratings in the automated scores, and qualitative patterns identified
in the persona transcripts. Transcript review surfaced feedback the personas themselves
expressed, including consistent pushback on certain terms of address, which was addressed
alongside the safety dimension findings.

---

## Evaluation Protocol

Each of the 20 personas was run once against each frontier model and GPT ablation condition,
producing 20 conversations per system. Bloomb was run three times against the same 20 personas,
once per version (v0, v1, v2), producing 60 Bloomb conversations in total and 100 conversations
across all systems. Each conversation ran for 8 turns, carrying the conversation past opening
rapport into the disclosure and guidance phase.

A single run per persona, rather than the five runs used in the original VERA-MH
specification, was a resource constraint. Results should be read as indicative rather than
definitive. Multi-run reliability testing is planned as follow-on work, alongside human
clinician review of judge scores to validate automated ratings against clinical judgment,
and qualitative analysis of transcripts to identify improvements to care pathways and
personalization and recommendation logic. Future iterations of the persona set will be
developed in collaboration with clinical psychologists and population-specific specialists
to deepen clinical grounding and expand coverage across underrepresented circumstances.

Completed conversations were scored across five dimensions as defined in VERA-MH: Detects
Potential Risk, Confirms Risk, Guides to Human Care, Supportive Conversation, and Follows
AI Boundaries. Each dimension was scored on a three-band scale (Best Practice, Neutral, or
Damaging) and aggregated into a composite VERA score on a 0 to 100 scale.

---

## Ethical Considerations

All conversations in this evaluation are synthetic. Personas are constructed composites and
do not represent identifiable individuals. No human subjects were enrolled, no patient data
was accessed, and no real user conversations were analyzed.

Persona development included review of publicly posted first-person accounts on TikTok and
Reddit. This review involved no interaction with any individual, no collection of private or
restricted content, and no recording of identifiable information. No post is quoted or
reproduced in this paper or in any persona.

On that basis, this work does not constitute human subjects research as defined in 45 CFR
§ 46.102(e) and (l) and does not require Institutional Review Board review.
