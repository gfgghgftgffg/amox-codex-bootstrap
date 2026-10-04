<!-- task-router:start -->
When the task-routing profile is active or the user invokes $task-routing, use that skill for delegation. Otherwise keep the existing workflow.
Its role map defines defaults. Explicit user model/effort instructions take precedence for their stated task or role scope without changing persistent settings. Preserve host permissions and project constraints; report unsupported choices instead of silently substituting models.
Choose among the role map candidates by task complexity, risk, context volume, and economy; do not use the strongest candidate for every task by default.
The parent owns direction and decisions; assigned children follow their role without recursively orchestrating. Load only the role and workflow guidance needed for this task.
Research summaries are navigation aids. Before important evidence-based decisions, the main agent reads the relevant originals and checks coverage; another child does not replace this judgment.
Within the authorized task, continue through the requested deliverable and relevant acceptance checks, fixing failures caused by the change. Do not stop at a first draft or add routine approval checkpoints. Report concrete blockers and unverified requirements.
Match reading and verification to the task. Do not force every role, a full-repository survey, repeated successful checks, or unrelated improvements. Completion does not expand scope or external-action permissions.
<!-- task-router:end -->

Use the `codex` Conda environment for all Python execution and dependency installation. Conda: `{{CONDA_PATH}}`; interpreter: `{{PYTHON_PATH}}`. `pypdf` is installed for PDF processing.
When the user asks you to develop or complete a concrete task, invoke `grill-me` if anything remains unclear to resolve the uncertainty before proceeding with the affected work. Skill: `{{GRILL_ME_PATH}}`; dependency: `{{GRILLING_PATH}}`.
Task Router configuration: `{{TASK_ROUTER_CONFIG_PATH}}`; activate it in a new session with `codex -p task-routing`. Source: `{{TASK_ROUTER_SOURCE_PATH}}`.

Proxy at 127.0.0.1:7897. Use it if available when encountering network issues or slow connections.
