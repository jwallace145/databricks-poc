# databricks-poc

A proof-of-concept Databricks workspace on AWS, focused on data governance and
visibility: Unity Catalog, central compute policies, audit logs and tags on
every resource.

The workspace is provisioned by
[jaws](https://github.com/jwallace145/jaws)
from [`jaws.yaml`](jaws.yaml). This
repository only says what the project asks for: its compute policies and its
workspace users. The network, cost center, admins and guardrails are central.
See [docs/databricks.md](https://github.com/jwallace145/jaws/blob/main/docs/databricks.md).

## Contributing

Changes go through pull requests with one-line Conventional Commits; see
[CONTRIBUTING.md](CONTRIBUTING.md). The rules for coding agents are in
[AGENTS.md](AGENTS.md). Licensed under the [MIT License](LICENSE).
