# Data map

## 1. Lives in Forgejo


| Data                                                                      | Forgejo object                                                                                      |
| ------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| Accounts, passwords, 2FA, email, avatar                                   | User                                                                                                |
| Organisation                                                              | Organization, private                                                                               |
| Staff roles (admin, manager, observer at org, contest, task)              | Team membership, 3 teams per scope                                                                  |
| Approved contestant or team                                               | Write collaborator on desk repo and submission repos                                                |
| Contest config: dates, state, registration rules, leaderboard definitions | `contest.yaml` in the contest repo                                                                  |
| Task content: statement, tests, checker, `task.yaml`, stages, limits      | Task repo                                                                                           |
| Task publication                                                          | Tag `published/<n>` on the task repo                                                                |
| Submission                                                                | Tag `submission/<n>` on the submission repo                                                         |
| Verdict and score                                                         | Grading pipeline run on the task repo (Woodpecker) and its `verdict.json` result                    |
| Announcements                                                             | Issue labelled `announcement` on the contest or task repo                                           |
| Clarifications and answers                                                | • Issue labelled `clarification` on the asker's desk or submission repo • Answer is a comment on it |
| Who may push or read a repo                                               | Enforced by Forgejo at push and clone                                                               |




## 2. Must live in Unicon


| Table              | Why Forgejo cannot hold it                                                                                                                          |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| `sessions`         | Login cookie, plus the user's Forgejo token (encrypted) so Unicon acts in Forgejo as that user                                                      |
| `participants`     | • No Forgejo object for a registration request before approval • Other info, e.g. personal time extension                                           |
| `teams`            | • Contest teams are not Forgejo teams, since org members can list all members and emails • Leader, join requests and pending members have no object |
| `invites`          | • No object • May target an email with no account yet                                                                                               |
| `entrant_repos`    | • Provisioning state of each contestant's desk and submission repos: pending, ready, failed • Forgejo only knows whether the repo exists            |
| `judgings`         | • Which submission: repo, tag, commit, entrant, task, time • Attempt number • Other info, e.g. which stage, selected for final                      |
| `uploads`          | Browser uploads in Garage awaiting a submit                                                                                                         |
| `jupyter_sessions` | Jupyter stuff                                                                                                                                       |




## 3. Possibly slow data

Some pages need many calls, e.g.

- Contest home: `contest.yaml` plus `task.yaml` and tags for every task, about 20 calls, times every contestant at contest start
- Leaderboard: one `GET /users/{id}` per entrant for names
- etc.

Needs testing later. If slow, add a short in-memory cache in the backend.
