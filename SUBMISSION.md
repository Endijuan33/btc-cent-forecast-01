# btc-cent-forecast-01 — SUBMISSION (prepared by subagent, submit pending parent)

- Competition: btc-cent-forecast-01 ($250), deadline **2026-11-15T08:00:00Z (15:00 WIB)**
- Repo: https://github.com/Endijuan33/btc-cent-forecast-01
- Commit: `ce138925dc0c8039f0eb2390db13bc30348ec482` (branch main)
- Kit: `~/workspace/makefun/kits/btc-cent-forecast-01-kit` (level 13 CLI)
- Method: damped 60-min momentum — `last * exp(0.25 * meanLogRet60 * 240)`,
  capped at +/-1% of last price. Practice MAE **$334.91** vs persistence
  **$470.55** (answers recovered from next case's checkpoint close, 5 cases).
  Deterministic, Node 22 stdlib only, verified locally.
- Local files: `~/workspace/makefun/btc-cent-forecast-01/` (main.ts, README.md, LICENSE)
- Bundle: `~/workspace/makefun/btc-cent-forecast-01-bundle.tar.gz`
  (WRITTEN 14:56 WIB, 84,475 bytes, sha256 e12c937a7c461897014e4226da8bbcf3cfff9090835c3964f6920880168b809d —
  1 session, 32 turns, 104 lines kept; **0 usage rows attached**, so this bundle
  WILL BE REJECTED as-is. Re-bundle per steps below.)
- Bundle flags that worked: `--no-discover --session <my session file>
  --prompt-file ~/workspace/makefun/btc-cent-prompt.txt --prompt-origin handed-off
  --prompt-via "main agent delegated btc-cent-forecast-01 entry, deadline 15:00 WIB"
  --mcp none --harness muse-app --harness-version 1.3 --provider meta
  --model muse-spark-1.3 --effort default`
- My session file: `~/agents/agent-74e67135-1e21-48a4-a2a4-623516e79306/sessions/74e67135-1e21-48a4-a2a4-623516e79306.jsonl`
  (agent_id 74e67135-1e21-48a4-a2a4-623516e79306)
- Parent session: agent_id d07fdac9-0616-4de9-9112-e8f7a5b5a86b.
  The bundle ITSELF says: run bundle from the top-level agent, with the SELECT
  over its own agent_id AND each subagent's, taking their sessions.
- WARNING: repo shows `repo.dirty` (SUBMISSION.md untracked in the work dir).
  Do NOT commit/push SUBMISSION.md once the claim code is in it (claim code
  must stay private); the dirty flag is only recorded, check will judge it.
- Claim code: NOT YET ISSUED — fill in after submit.

## Why the subagent could not submit itself

Subagent token-usage rows are only written to muse.db when the subagent's run
completes, so `makefun check` run by the subagent fails `thinking_priced`
(0 usage rows). The parent MUST do these steps immediately after this
subagent finishes (rows for agent 74e67135-1e21-48a4-a2a4-623516e79306 appear
then):

```sh
# 1. Fetch usage rows (muse.db tool) for BOTH agent ids and write unchanged,
#    one JSON per line:
#    SELECT u.agent_id, u.message_id, u.created_at, u.input_tokens,
#           u.output_tokens, a.model FROM agent.agent_message_token_usage u
#    JOIN agent.agents a ON a.agent_id = u.agent_id
#    WHERE u.agent_id IN ('d07fdac9-0616-4de9-9112-e8f7a5b5a86b',
#                         '74e67135-1e21-48a4-a2a4-623516e79306')
#    ORDER BY u.created_at DESC LIMIT 500
#    -> ~/workspace/makefun/muse-usage-btc-cent.jsonl
#    (Subagent rows appear only once this subagent run completes — i.e. NOW.)

# 2. Re-bundle FROM THE TOP-LEVEL AGENT, taking both sessions, with usage rows:
cd ~/workspace/makefun/kits/btc-cent-forecast-01-kit
node cli/makefun.mjs bundle --repo ~/workspace/makefun/btc-cent-forecast-01 \
  --out ~/workspace/makefun/btc-cent-forecast-01-bundle.tar.gz \
  --no-discover \
  --session ~/agents/agent-d07fdac9-0616-4de9-9112-e8f7a5b5a86b/sessions/d07fdac9-0616-4de9-9112-e8f7a5b5a86b.jsonl \
  --session ~/agents/agent-74e67135-1e21-48a4-a2a4-623516e79306/sessions/74e67135-1e21-48a4-a2a4-623516e79306.jsonl \
  --muse-usage ~/workspace/makefun/muse-usage-btc-cent.jsonl \
  --prompt-file ~/workspace/makefun/btc-cent-prompt.txt --prompt-origin handed-off \
  --prompt-via "main agent delegated btc-cent-forecast-01 entry, deadline 15:00 WIB" \
  --mcp none --harness muse-app --harness-version 1.3 --provider meta \
  --model muse-spark-1.3 --effort default
# (If the parent's own session already opens with the user's message, the
#  --prompt-file may be unnecessary; keep the other flags. Adjust --session
#  paths to the parent's actual session file location if different.)

# 3. Check:
node cli/makefun.mjs check --kit ~/workspace/makefun/kits/btc-cent-forecast-01-kit \
  --repo ~/workspace/makefun/btc-cent-forecast-01 \
  --commit ce138925dc0c8039f0eb2390db13bc30348ec482 \
  --transcripts ~/workspace/makefun/btc-cent-forecast-01-bundle.tar.gz

# 4. Submit (before 15:00 WIB):
node cli/makefun.mjs submit --kit ~/workspace/makefun/kits/btc-cent-forecast-01-kit \
  --repo ~/workspace/makefun/btc-cent-forecast-01 \
  --commit ce138925dc0c8039f0eb2390db13bc30348ec482 \
  --transcripts ~/workspace/makefun/btc-cent-forecast-01-bundle.tar.gz \
  --keypair ~/workspace/makefun/makefun-keypair.json
```

If `submit` flags differ, run `node cli/makefun.mjs submit --help` first.
Save the claim code here and report the submission id to Endcore.
