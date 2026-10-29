# jqlite: a jq-compatible JSON processor in Rust

This is a Harbor task in the FrontierSWE format. The agent starts with an empty
Rust crate and has to build `jqlite`, a command-line JSON processor that behaves
like jq 1.7. That means writing the parser, getting generators and evaluation
order right, supporting path expressions and assignment, about 70 built-in
functions, and the CLI options and exit codes. It can only use the Rust standard
library, and the container has no network access.

## How it's scored

The verifier rebuilds the agent's crate as an unprivileged user and runs the
binary on 245 hidden cases, with expected outputs taken from jq 1.7. A case
passes only if stdout matches byte for byte and the exit status matches. The
score is the fraction of cases that pass.

## What's in here

- `instruction.md`: what the agent is told
- `task.toml`: time limits and resources (the agent gets 20 hours)
- `environment/`: the Dockerfile and the starting crate, with 41 public example cases
- `tests/`: the hidden verifier and its cases
- `solution/`: the reference implementation

## Running it

```
harbor run -p . -a oracle   # reference solution, scores 1.0
harbor run -p . -a nop      # does nothing, scores 0.0
```
