# Gestor Gastrô HML

This overlay contains the first HML package for Gestor Gastrô:

- Admin
- Shop

## Required prerequisites before ArgoCD sync

- The namespace `umami-gestor-gastro-hml` must exist.
- The real application secret for Admin must be created outside GitOps.
- The real `ghcr-pull-secret` must be created in `umami-gestor-gastro-hml` before sync so the private images can be pulled.

## Image tag status

The manifests currently reference:

- `ghcr.io/umamii-tech/gestor-gastro-admin:hml-d6fc8d9`
- `ghcr.io/umamii-tech/gestor-gastro-shop:hml-d6fc8d9`

That tag is marked as pending placeholder build verification and should not be treated as a fully validated HML release until the runtime secrets and pull secret are in place.

## Routing note

Admin is routed through `/admin` and the ingress applies a StripPrefix middleware. The Admin health check is available at `/api/health`, which is used for probes.
