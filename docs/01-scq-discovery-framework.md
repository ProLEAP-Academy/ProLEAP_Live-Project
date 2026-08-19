# SCQ Discovery Framework

## Purpose

SCQ is a structured way to discover the real problem before proposing a technical solution.

- **S - Situation:** What is happening today?
- **C - Complication / Challenge:** Why is the current state insufficient?
- **Q - Question:** What must be answered to design a successful solution?

The older SCQ material focused mainly on cost, time and tool sprawl. The modern framework retains that intent but adds measurable outcomes, stakeholders, constraints, evidence and decision criteria.

## The rule

Do not start SCQ with a preferred technology.

Bad discovery:

> We should deploy Kubernetes. What Kubernetes features do you need?

Better discovery:

> What workload problem exists today, who experiences it, how often, what is the impact, and what result would make the project successful?

Technology belongs after the problem is understood.

## Situation

Capture factual current-state information.

### Questions

- Who owns the process/system?
- Who uses it?
- What business process does it support?
- What systems/tools are currently involved?
- What is manual vs automated?
- How frequently does the process run?
- What volumes are handled?
- What environments exist?
- What dependencies are external?
- What security or regulatory constraints exist?
- What data is processed and how sensitive is it?
- What evidence exists: logs, tickets, costs, cycle times, outage records, spreadsheets, architecture diagrams?

### Output

A short current-state statement based on facts, not assumptions.

Example:

> The analytics team receives a ZIP archive containing multiple Excel workbooks each month. An analyst manually extracts quarterly values from Empirical and Regression sheets, combines them into an output workbook and updates a database. The process depends on spreadsheet interpretation and currently has no automated validation, rerun control or operational monitoring.

## Challenge / Complication

Describe the measurable impact of the current situation.

Use these dimensions where applicable:

- **Time:** cycle time, waiting time, deployment time, recovery time.
- **Cost:** infrastructure cost, license cost, operational labor, rework.
- **Quality:** errors, inconsistent output, missing validation.
- **Reliability:** outages, manual recovery, fragile dependencies.
- **Security:** exposed credentials, insecure transfer, excessive privileges.
- **Scale:** inability to handle volume, concurrency or growth.
- **Visibility:** lack of metrics, logs, ownership or audit trail.
- **Delivery:** delayed releases, manual handoffs, unrepeatable environments.

A challenge must explain why the project matters.

Example:

> Manual extraction is slow, difficult to audit and vulnerable to incorrect cell/sheet interpretation. Same-day reruns can create duplicate or inconsistent data, and failures are not centrally observable. The business requires a repeatable end-to-end process that completes within 30 minutes and preserves data integrity.

## Question

Questions must close information gaps that materially affect design or acceptance.

### Business questions

- What outcome is mandatory?
- How is success measured?
- What is the acceptable failure rate?
- What is the maximum acceptable processing time?
- Which requirements are Must vs Should?

### Data questions

- What is the authoritative source?
- Can source schemas/layouts change?
- How are duplicates identified?
- What is the retention period?
- What is considered sensitive data?
- What is the expected data volume and growth?

### Integration questions

- Which APIs, repositories, servers or databases are available?
- What authentication mechanisms are supported?
- What rate limits, quotas or maintenance windows apply?
- What network restrictions exist?

### Operational questions

- Who responds to failures?
- What alerts are actionable?
- What recovery time is acceptable?
- How should reruns work?
- What backup/restore capability is required?

### Delivery questions

- Which environments are required?
- What is the change-approval process?
- What CI/CD platform is allowed?
- What is the rollback expectation?

## SCQ output format

Each discovery should end with this concise structure:

### Situation
3-8 factual statements describing current state.

### Challenge
3-8 statements explaining impact and why change is needed.

### Key Questions
A prioritized list of unanswered questions.

### Desired Outcome
A measurable statement such as:

> Automate ingestion and transformation of all supported source workbooks, publish validated output and database records, complete a normal run in <=30 minutes, support safe reruns, and provide enough telemetry for an operator to diagnose failures without reading source code.

### Constraints
Budget, time, technology, data, network, compliance, availability or team constraints.

### Assumptions
Facts temporarily assumed true and requiring validation.

### Out of Scope
Explicit exclusions.

### Decision Criteria
How alternatives will be compared: security, simplicity, cost, portability, recovery, performance, maintainability, etc.

## Discovery quality gate

SCQ is complete only when the team can answer:

- What problem are we solving?
- Who benefits?
- What evidence shows the problem exists?
- What measurable outcome defines success?
- What constraints materially shape the solution?
- What is still unknown?
- What is explicitly out of scope?

If these cannot be answered, implementation is premature.

## Example - tool sprawl

### Situation
A team uses several independent tools that produce overlapping operational data. Each tool has separate access control, dashboards and maintenance overhead.

### Challenge
Costs are duplicated, incident investigation requires switching between tools, ownership is unclear and data correlation is slow.

### Questions
- Which capabilities are genuinely unique?
- Which tools are contractually required?
- What are license and operational costs?
- Which data sources are business critical?
- What retention and compliance requirements exist?
- Can open-source or consolidated alternatives satisfy the same controls?
- What migration risk is acceptable?

### Desired outcome
Reduce duplicated operational tooling without reducing required visibility, security or supportability.

## Template

Use [`../templates/SCQ_TEMPLATE.md`](../templates/SCQ_TEMPLATE.md) for project work.
