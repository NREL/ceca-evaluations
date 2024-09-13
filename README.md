# Evaluation Library

The Clean Energy Cybersecurity Accelerator :tm: (CECA) conducts evaluations to assess technologies under test. This library contains the evaluation plans that have been completed for CECA.

CECA operates in cohorts of technologies under test. Each cohort has a **Prioritized Threat**. Each plan was created for a specific cohort. The goal for each plan is to focus on the prioritized threat and how it relates to the technologies under test. As such, each plan will be structured differently and may make assumptions regarding stages that may not be relevant for the given cohort, such as initial access, privilege escalation, etc. Each evaluation plan contains one or more scenarios. Each scenario emulates all or a portion of the given prioritize threat.

## Structure of Repository

Each directory represents one evaluation plan. The name of the directory is based on the name of the prioritized threat or the focus of a given cohort. The name can either be threat actor based (such as Sandworm) or a broad category that a threat might abuse such as weak authentication.

| Cohort | Prioritized Threat | Plan |
| ------ | ------------------ | ---- |
| CH1    | Strong Authentication and Authorization | *evaluation procedures not made public* |
| CH2    | Hidden Risks due to Incomplete System Visibility | [asset-identification](/asset-identification/README.md)
