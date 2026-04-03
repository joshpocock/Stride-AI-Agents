# CLAUDE.md Optimizer Prompt

Use this prompt to reduce a bloated CLAUDE.md to its essential form. Paste it into Claude Code (or any agent) along with your current CLAUDE.md file.

---

## The Prompt

```
Review the CLAUDE.md file in this project and optimize it using these rules:

DELETE anything that:
- Claude can discover by reading the codebase (file structure, tech stack detection, standard patterns)
- Is a standard language/framework convention Claude already knows (PEP 8, REST conventions, React best practices)
- Is a code style rule that a linter or formatter should handle instead
- Is detailed documentation that belongs in a separate doc file (reference it with a pointer instead)
- Is deployment, CI/CD, or environment setup docs (not relevant to every coding task)
- Lists environment variables (security risk if CLAUDE.md is in git)
- Describes project history, team members, sprint methodology, or organizational context
- Duplicates information from package.json, README, or other existing files
- Would NOT apply to every single task Claude works on in this project

KEEP only:
- Commands Claude cannot guess (custom scripts, non-obvious test runners)
- Code standards that DIFFER from what Claude would do by default
- Architectural decisions Claude would get wrong without being told
- Workflow rules (branch naming, PR conventions, commit format)
- Common mistakes / gotchas that have actually happened before
- Explicit "NEVER do X" rules for dangerous or costly mistakes
- Pointers to detailed docs: "For X, see @docs/X.md" (NOT the docs themselves)

FORMAT the result as:
1. Commands (5-8 lines)
2. Code Standards (5-10 lines, only non-obvious ones)
3. Architecture (3-5 lines, just enough to orient)
4. Workflow (3-5 lines)
5. Common Mistakes (3-5 lines, failure-driven)
6. Do Nots (3-5 lines, NEVER/MUST language)

Target: under 80 lines. Absolute max: 200 lines.

For anything you delete that IS valuable but not universally applicable, suggest moving it to a separate file in an agent_docs/ directory and add a one-line pointer in the CLAUDE.md.

Show me:
1. The optimized CLAUDE.md
2. A list of what you removed and why
3. Any suggested agent_docs/ files to create
```

---

## Expected Results

A bloated 300+ line file should reduce to 50-80 lines. The prompt enforces:
- The ETH Zurich finding: only include what Claude can't discover on its own
- The HumanLayer principle: never send an LLM to do a linter's job
- Progressive disclosure: point to docs instead of including them
- The instruction budget: every line competes with every other line

## For the Video Demo

1. Open the bloated example file on screen
2. Paste this prompt into Claude Code
3. Watch it reduce the file in real time
4. Walk through the result explaining what stayed and why
5. Show the suggested agent_docs/ files as the progressive disclosure payoff
