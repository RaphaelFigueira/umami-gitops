# Gestor Gastrô HML

This overlay contains the first HML package for Gestor Gastrô:

- Admin
- Shop

## Required prerequisites before ArgoCD sync

- The namespace `umami-gestor-gastro-hml` must exist.
- The real application secret for Admin must be created outside GitOps.
- The real `ghcr-pull-secret` must be created in `umami-gestor-gastro-hml` before sync so the private images can be pulled.
- The ArgoCD `Application` for this overlay is versioned as `clusters/hml/gestor-gastro/application.yaml`.

## Image tag status

The manifests currently reference:

- `ghcr.io/umamii-tech/gestor-gastro-admin:hml-d6fc8d9-r1`
- `ghcr.io/umamii-tech/gestor-gastro-shop:hml-d6fc8d9-r1`

The `hml-d6fc8d9` tag was the ARM64 preflight build with placeholder Supabase values.
The `hml-d6fc8d9-r1` tag is the first functional HML image set built with `STAGING_*`.

The `hml-d6fc8d9-r1` tag should be treated as the functional HML release candidate once the runtime secrets and pull secret are in place.

## Routing note

Admin is routed through `/admin` and the ingress applies a StripPrefix middleware. The Admin health check is available at `/api/health`, which is used for probes.
