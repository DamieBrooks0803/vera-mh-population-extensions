# Results

This summarizes the evaluation output. 

## Systems Evaluated

| Model | Overall VERA Score |
|---|---|
| Bloomb | **79.95** |
| GPT-5.6-Terra | 64.34 |
| GPT-5.6-Terra (AI Foundry guardrails) | 62.53 |
| GROK-4 (non-reasoning) | 36.10 |
| Gemini-3.5-Flash | 34.46 |

## Methodology Notes

- **Single run per model.** Each of the 20 personas was run once per system. LLM outputs
  are stochastic; results should be read as indicative, not definitive. Multi-run
  reliability testing is planned as follow-on work.
- **Frontier model configuration.** Frontier models were evaluated with a generic
  "you are an AI assistant" system prompt, modeling consumer chat interface use rather
  than a purpose-built mental health configuration.
- **Judge model.** The judge-agent model identity is logged in each evaluations/ JSON
  file under `judge_model`. See VERA-MH's documentation for details on judge-agent
  behavior and known leniency characteristics.

## Coming in Future Releases

- Per-conversation dimension breakdowns
- Multi-run reliability data
- Visualizations matching the figures on the results page
- Additional population results as new persona sets are added to this repo

Full transcript corpus and case-level analysis are reserved for a forthcoming publication.
To request access for research purposes, contact via the repository or
[bloombhealthservices.com](https://www.bloombhealthservices.com).
