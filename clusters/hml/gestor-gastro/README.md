# Gestor Gastro HML

This overlay contains the first HML package for Gestor Gastro:

- Admin
- Shop

## Required prerequisites before ArgoCD sync

- The namespace `umami-gestor-gastro-hml` must exist.
- The real application secret `gestor-gastro-admin-secrets` must be created outside GitOps.
- The real `ghcr-pull-secret` must be created in `umami-gestor-gastro-hml` before sync so the private images can be pulled.
- The ArgoCD `Application` for this overlay is versioned as `clusters/hml/gestor-gastro/application.yaml` and must be bootstrapped manually or by a higher-level app-of-apps into the ArgoCD namespace `umami-argocd-hml`.
- This `Application` is intentionally excluded from the overlay `kustomization.yaml` so it is not applied into the workload namespace.

## Image tag status

The manifests currently reference:

- `ghcr.io/umamii-tech/gestor-gastro-admin:hml-d6fc8d9-r1`
- `ghcr.io/umamii-tech/gestor-gastro-shop:hml-d6fc8d9-r1`

The `hml-d6fc8d9` tag was the ARM64 preflight build with placeholder Supabase values.
The `hml-d6fc8d9-r1` tag is the first functional HML image set built with `STAGING_*`.

The `hml-d6fc8d9-r1` tag should be treated as the functional HML release candidate once the runtime secrets and pull secret are in place.

## Routing note

Admin is routed through `/admin` and the ingress applies a StripPrefix middleware. The Admin health check is available at `/api/health`, which is used for probes.

## Cloudflare Access

Cloudflare Access must protect `gestor-gastro-hml.umamitech.net.br` before the hostname is exposed publicly.
