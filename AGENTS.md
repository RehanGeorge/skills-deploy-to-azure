# Repository agent guidance

## Repository role

This is a completed GitHub Skills “Deploy to Azure” exercise. The small JavaScript game is only the deployment payload; the primary learning surface is the label-driven GitHub Actions workflow sequence under `.github/workflows/` and the companion steps under `.github/steps/` and `LAB_STEPS.md`.

Preserve completed course state and evidence. Do not reset the exercise workflows or reintroduce step automation unless the task explicitly asks to replay the course.

## Application verification

```bash
npm ci
npm test
npm run build
docker build -t skills-deploy-to-azure:local .
```

Keep source in `src/`, test behavior in `__test__/`, and generated build output out of Git unless the course explicitly treats it as an artifact.

## Workflow rules

- Keep staging and production environment jobs distinct and preserve their approval/environment boundaries.
- Keep label filters, artifact handoff, Azure setup, deployment, and destroy steps aligned with the lesson contract.
- Pin or deliberately version third-party actions; avoid floating unreviewed action references.
- Use repository/environment secrets for credentials. Never commit Azure credentials, publish profiles, subscription IDs tied to private accounts, or generated kube/cloud configuration.
- Treat `.github/steps/` as course-controller content; do not casually edit it while changing the sample application.

## External action boundary

The Azure setup, spin-up, staging, production, and destroy workflows create or remove real cloud resources and may incur cost. Do not dispatch them, add labels that trigger them, approve environments, or destroy resources as routine verification. Explicitly confirm the target subscription, environment, and cleanup plan before any live run.
