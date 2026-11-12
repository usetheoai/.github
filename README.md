# usetheoai/.github

Shared GitHub Actions workflows for the `usetheoai` repositories.

## build-publish

`.github/workflows/build-publish.yml` builds a container image and pushes it to GHCR, and to Amazon ECR when the caller passes `ecr_registry` and `aws_role_arn`. It can gate the image on Trivy (CRITICAL and HIGH), attach an SBOM and SLSA provenance, and sign it with keyless cosign.

It lives in this public repository because a public repository cannot call a reusable workflow from a private one. Call it pinned to a commit SHA:

```yaml
jobs:
  image:
    permissions:
      contents: read
      packages: write
      id-token: write
      attestations: write
    uses: usetheoai/.github/.github/workflows/build-publish.yml@<commit-sha>
    with:
      image: my-service
      dockerfile: ./Dockerfile
```

The inputs and their defaults are documented at the top of the workflow.
