# backend-oneshots

Baseline experiments for comparing [`rama-ai-learn`](https://github.com/okwalerie/rama-ai-learn) against
conventional backend generation, reproducing
[Constraint Decay: The Fragility of LLM Agents in Backend Code Generation](https://arxiv.org/abs/2605.06445).

`constraint-decay/` is the paper's reproducibility package
([francdente/constraint-decay](https://github.com/francdente/constraint-decay)), pinned as a submodule.

## Orbs

`.agents/setup` installs Docker Compose, enables Docker, runs `uv sync` for the harness, writes
`constraint-decay/.env` with orb-local task and result paths, and pre-builds the `apibench/uv`,
`apibench/node`, and `apibench/newman` images plus `postgres:16`. `.agents/resume` starts Docker.

Provide `LLM_API_KEY` and `LLM_MODEL` (LiteLLM naming, e.g. `anthropic/<model>`) as Amp secrets or
environment variables, then:

```bash
cd constraint-decay
uv run main.py --agent mini_swe_sdk --task uv/uv-flask-openapi-unconstrained.json --runs 1
```
