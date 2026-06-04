# Cachelet Exercise: Observability and Deployment

## Context

Cachelet is a small in-memory cache service exposed over HTTP. The full code is in this repo; read the README and skim the source before you start. The surface area is intentionally small (~400 LOC).

Today, cachelet has no production observability and nothing wiring it into a Kubernetes deployment. Your job is to add both, well enough that an oncall engineer could run it.

## Your task

Add the following:

1. **A Prometheus metrics endpoint at `GET /metrics`.** Expose whichever signals you think matter for running this service in production.

2. **A liveness endpoint at `GET /healthz` and a readiness endpoint at `GET /readyz`.** Decide what each should mean for cachelet.

3. **A `Dockerfile`** that builds and runs cachelet. It should work end-to-end:
   ```
   docker build -t cachelet .
   docker run -p 8080:8080 cachelet
   ```

4. **Kubernetes manifests** under `deploy/` that run cachelet on a cluster. Include whatever you think a production deployment needs. Assume a vanilla cluster with Prometheus already running.

For each of these, the brief tells you *what* to add; the *how* is up to you. We are evaluating your judgment, including what you choose to do and what you choose not to do.

## Constraints

- Do not change the existing cache HTTP API (`GET/PUT/DELETE /cache/{key}`, `GET /stats`).
- Existing tests must continue to pass. Add tests for what you add.
- `go test -race ./...` must be clean.
- `kubectl apply --dry-run=client -f deploy/` must succeed.
- Default behavior with no configuration changes should be unchanged.

## Submission

Open a PR against `main`.

Your PR description must include an **"Operating this service"** section covering:

- What a healthy state looks like
- Two or three things you would alert on
- What you would check first if one of those alerts fired

This section is part of the evaluation. Keep it to a few paragraphs; we are not asking for a full runbook.

## Time and scope

Budget around 4 hours. If you find yourself well past that, stop and submit what you have with a short note on what you would do next.

Resist scope creep. Do not add features beyond what is specified above. We care more about the depth of your thinking on the things we asked for than the breadth of things you added.

## Using AI tools

You may use any AI coding assistant (Claude Code, Cursor, Copilot, ChatGPT, etc.). We expect you will, and that mirrors how the role actually works.

You should be able to defend every line that ends up in your PR. The follow-up conversation will focus on specific decisions in the code, and "the agent wrote it that way" is not an answer we can take. Treat the agent's output as a draft you review and edit, not as your submission.

## What happens next

After you submit, we will schedule a 45 minute conversation. It is code-review shaped: we walk through your PR together and discuss the choices you made.

Good luck. Reach out if anything in this brief is ambiguous.
