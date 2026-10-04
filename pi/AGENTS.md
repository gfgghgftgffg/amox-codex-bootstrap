Python execution and dependency installation utilize the Conda `codex` environment; Conda path: `{{CONDA_PATH}}`, interpreter path: `{{PYTHON_PATH}}`. `pypdf` is installed for PDF processing.

Proxy at 127.0.0.1:7897. Using it if encounter network issues or slow speed.

<!-- pi-task-router:start -->
Task Router for Pi is opt-in. When the user invokes /skill:task-routing or applicable instructions explicitly enable it, the coordinating parent follows that skill and its generated tr_* role map. Otherwise keep the existing workflow.
Installation alone does not authorize delegation. An assigned child follows its role contract and does not activate parent routing or launch further agents.
Use pi-subagents for execution, not builtin role substitutions or a separate runner. Explicit task-scoped model/thinking choices take precedence; preserve host permissions and report unsupported routes.
<!-- pi-task-router:end -->
