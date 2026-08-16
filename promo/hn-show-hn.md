# Show HN: Enough – a 300-line AI coding workflow skill with 5 hard gates

I got tired of AI assistants that happily reinvent wheels, start coding in the wrong direction, or claim “done” without real evidence. So I packaged the habits of a careful engineer into a tiny, tool-agnostic Agent Skill (works with Codex, Claude Code, OpenCode, and more).

It does not implement anything. It orchestrates and gates:

1. No reuse decision → no custom building. Before any code, search GitHub and output “adopt / extend / borrow / build” with an evidence level (E1/E2/E3).
2. No design approval → no code. One blocking question at a time; reasoned defaults for the rest.
3. No proven vertical slice → no expanded scope. Prove “launch → action → persist → display” first.
4. No criterion-by-criterion acceptance evidence → no “done”. Each approved acceptance criterion gets verified / partial / unverified status.
5. No security & release check → no shipping.

The whole thing is 4 files, ~300 lines, zero dependencies. If a supporting capability (brainstorming, verification planning, code index) is missing, it degrades to an equivalent simplified flow instead of failing.

It has been shaped by real projects: one end-to-end case (a privacy-first journaling Android app) is included, including the parts that were NOT verified — because “done” should mean something.

Install:

```bash
gh skill install zhizhixia/enough enough --agent codex --scope user
# or
npx skills add zhizhixia/enough --yes
```

Repo: https://github.com/zhizhixia/enough

Happy to discuss where the gates are too strict or too loose.