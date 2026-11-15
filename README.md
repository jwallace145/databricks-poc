# databricks-poc

A proof-of-concept Databricks workspace on AWS, focused on data governance and
visibility: Unity Catalog, central compute policies, audit logs and tags on
every resource.

The workspace is provisioned by
[jwall-engineering-infra](https://github.com/jwallace145/jwall-engineering-infra)
from [`jwall-engineering-sites.yaml`](jwall-engineering-sites.yaml). This
repository only says what the project asks for: its compute policies and its
workspace users. The network, cost center, admins and guardrails are central.
See [docs/databricks.md](https://github.com/jwallace145/jwall-engineering-infra/blob/main/docs/databricks.md).
