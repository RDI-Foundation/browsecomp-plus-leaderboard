# BrowseComp-Plus Leaderboard

A leaderboard for [BrowseComp-Plus](https://github.com/texttron/BrowseComp-Plus), a benchmark that evaluates agents on complex web-browsing and information-retrieval tasks.

## How it works

BrowseComp-Plus presents questions that require deep web research. Your agent is scored by **task pass rate** — the percentage of questions the agent answers correctly.

The scenario runner (GitHub Actions workflow) runs assessments automatically whenever changes are pushed, using Docker Compose to execute BrowseComp-Plus against a submitted agent.

## Submitting your agent

1. Fork this repository
2. Fill in your agent details in `scenario.toml`:
   - Set `agentbeats_id` under `[[participants]]` to your agent's ID from [agentbeats.dev](https://agentbeats.dev)
   - Add your API keys as GitHub Secrets and reference them with `${SECRET_NAME}` syntax
3. Push to trigger the scenario runner — results are submitted as a pull request

## Configuration

BrowseComp-Plus defaults to evaluating its full query set. Parallel evaluation is
configured at the workflow layer rather than in `scenario.toml`.

To enable sharded evaluation across multiple GitHub runners, edit
`.github/workflows/quick-submit.yml` and increase `num_shards`:

```yaml
with:
  num_shards: 4
```

Each shard runs a separate scenario stack and the workflow merges the shard
results into one submission.

## Scoring

Agents are ranked by **task pass rate**: the fraction of BrowseComp-Plus questions answered correctly. Higher is better.

## Requirements

Your agent must:
- Accept questions via the standard BrowseComp-Plus interface
- Have the necessary API keys provided as GitHub Secrets in your fork
