## Repos y versionado

- GitHub
- GitLab
- Bitbucket

## Estrategia de ramas

- Trunk-based
- GitFlow
- Release branches (si aplica)

## CI

- GitHub Actions
- GitLab CI
- CircleCI
- Jenkins (legacy)

## CD / Deploy

- GitHub Actions deploy
- Argo CD (GitOps)
- Flux CD
- Spinnaker

## Infraestructura (dónde corre)

- Vercel / Netlify (frontend)
- AWS (ECS / EKS / Lambda)
- GCP (Cloud Run / GKE / Functions)
- Azure (App Service / AKS)
- On-prem (raro)

## Container runtime

- Docker
- containerd

## Orquestación (si aplica)

- Kubernetes (EKS/GKE/AKS)
- ECS
- Nomad

## IaC (Infrastructure as Code)

- Terraform
- Pulumi
- AWS CDK
- CloudFormation
- Helm (K8s)

## Entornos

- Local
- Dev
- Staging
- Prod
- Preview environments (por PR)

## Secrets management

- GitHub Secrets
- AWS Secrets Manager
- GCP Secret Manager
- Vault
- Doppler

## Observabilidad

- Logs: ELK / OpenSearch, Loki
- Metrics: Prometheus + Grafana
- Tracing: OpenTelemetry + Jaeger/Tempo
- APM: Datadog / New Relic
- Error tracking: Sentry

## Monitoreo / Alertas

- Grafana Alerting
- Datadog monitors
- PagerDuty / Opsgenie
- Slack alerts

## Networking

- DNS: Route53 / Cloudflare DNS
- CDN: Cloudflare / CloudFront / Fastly
- Load balancer: ALB/NLB / Ingress NGINX
- WAF: Cloudflare WAF / AWS WAF
- TLS/SSL: ACM / Let’s Encrypt

## Seguridad (DevSecOps)

- SAST: CodeQL / SonarQube / Deepsource
- Dependency scan: Dependabot / Snyk
- Secret scan: Gitleaks
- Container scan: Trivy
- SBOM: Syft/Grype

## Calidad / Policies

- Branch protection rules
- Required reviews
- Required status checks
- Conventional commits
- Semantic versioning

## Artefactos / Registry

- Docker Hub
- GHCR (GitHub Container Registry)
- ECR (AWS)
- GCR/Artifact Registry (GCP)

## Bases de datos (operación)

- Backups automáticos
- Point-in-time recovery (PITR)
- Migrations en pipeline
- Read replicas (si aplica)

## Release / Rollback

- Blue/Green
- Canary releases
- Feature flags (para rollout)
- Rollback automático

## Performance / Edge

- Edge functions (Vercel/Cloudflare)
- Caching rules
- Image optimization pipeline