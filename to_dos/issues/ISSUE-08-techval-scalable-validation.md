# ISSUE-08: Plan scalable support for extraction validation

## What to do

- Add a scalable complement to manual extraction validation where useful.
- Use a staged validation design in which manual validation remains primary, but stronger LLM re-extraction and LLM-as-judge checks provide structured support.

## How to do it

- Decide which stronger models and LLM-as-judge setup are scientifically defensible for this paper.
- Position them as support for manual review, not as a replacement for all human inspection.
- Describe it in `SCIDATA_26_SR4ALL/scidata--sr4all-part4.tex`.

## Definition of done

- The validation plan includes a scalable support component if needed.
- Its purpose and limits are stated clearly.
- The paper does not overclaim what automated judging proves about extraction correctness.
