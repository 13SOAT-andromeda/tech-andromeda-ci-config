# 13SOAT-andromeda/tech-andromeda-ci-config

Reusable GitHub Actions workflows e composite actions compartilhados entre os repositórios do projeto `video-processor`.

Consumidores referenciam por tag (`@v1`), nunca por `@main`/`@master` — ver `docs/superpowers/specs/2026-07-25-cicd-pipelines-design.md` e `docs/superpowers/plans/2026-07-26-cicd-pipelines-implementation.md` (repo `video-processor-specs`) para o desenho completo.

## Reusable workflows

- `.github/workflows/reusable-go-ci.yml` — build/vet/lint/testes/SAST/SonarCloud para repos Go.
- `.github/workflows/reusable-terraform-cd.yml` — fmt/validate/test/plan (PR) + apply (push) para repos Terraform.
- `.github/workflows/reusable-lambda-cd.yml` — build de imagem Lambda (sem provenance/SBOM) + push ECR + chama `reusable-terraform-cd.yml`.
- `.github/workflows/reusable-eks-cd.yml` — build + push ECR + `kubectl apply -k` para repos EKS/Kustomize.

## Composite actions

- `actions/setup-go-cached` — `actions/setup-go` com `go-version-file` e cache.
- `actions/configure-aws-session` — `aws-actions/configure-aws-credentials` com os 4 secrets padrão de sessão.
