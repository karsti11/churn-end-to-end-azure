# Proof plan

What we want to show, and the evidence for it.
Tick items off as the screenshots and results are captured.

| Claim | Evidence | Asset | Done |
|---|---|---|---|
| It makes money | Optimizer vs random and top-N targeting at several budgets, with stated assumptions | Revenue-vs-budget chart, table in README | [ ] |
| We understand it | Time-based split, calibrated probabilities, decision log | Architecture diagram, MLflow comparison, Unity Catalog lineage | [ ] |
| Failures are handled | Scripted scenarios below | Pipeline check failures, blocked promotion, drift dashboard, job history | [ ] |
| CI/CD works | PR -> dev, tag -> prod | GitHub Actions run, green badge | [ ] |
| Anyone can reproduce it | README quickstart, three commands | Timed fresh-clone run | [ ] |

## Failure scenarios

1. Bad data arrives - quality checks quarantine it.
2. Source schema changes - pipeline handles or flags it.
3. A worse model is trained - the gate keeps the current model.
4. Behaviour drifts - monitoring alerts and retraining starts.
5. A job fails - retry and notification.
6. Rollback - prod returns to the previous model with one command.
7. Missing permission on a new table - fixed through Terraform grants, not by clicking in the UI.
