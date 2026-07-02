# Access Tech — client site (Hirobius)

Single static `index.html` marketing site for Access Tech (forestry mulching / land
management). See `README.md` for stack + launch checklist, `docs/` for build anatomy
and SOPs, `BACKLOG.md` for the phased task narrative.

## Fleet hub
This repo is part of the Hirobius fleet. The operations hub is the
hirobius/ops repo: fleet state at /api/projects, consolidated tasks at
/ops/tasks (this repo's GitHub Issues sync there), current cross-project
state in docs/ai/HANDOFF.md (in ops). Conventions for every session here:
(a) track new work as GitHub Issues in THIS repo — never a local TODO
file; (b) before ending any session that changed project state, update
root status.json (updatedAt, phase, headline, next, blocked) — the ops
dashboard renders it; (c) read the ops HANDOFF before cross-project
decisions.
