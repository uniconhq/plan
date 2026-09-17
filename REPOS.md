# Repos


| Repo       | What it is                                                                | What it produces                                                                                                                      |
| ---------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| `backend`  | FastAPI API, background jobs, compiler, the Forgejo and Woodpecker client | one container image, plus `openapi.json` committed at the root                                                                        |
| `frontend` | React app                                                                 | static bundle, built from a pinned backend `openapi.json`                                                                             |
| `runner`   | grading harness, primitives, `unicon-worker`                              | `ghcr.io/uniconhq/grading`, `ghcr.io/uniconhq/worker`, and the contract files: plan, envelope and verdict schemas, primitive registry |
| `deploy`   | compose files, proxy, Forgejo and Woodpecker config, bootstrap scripts    | nothing. It pins versions of the other three and runs the end-to-end test                                                             |
| `plan`     | the 21 task issues and the milestones, nothing else                       | nothing                                                                                                                               |
| `proposal` | docs and this plan                                                        | nothing                                                                                                                               |


