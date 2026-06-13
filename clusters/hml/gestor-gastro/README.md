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
- `ghcr.io/umamii-tech/gestor-gastro-shop:hml-d6fc8d9-r2`

The `hml-d6fc8d9` tag was the ARM64 preflight build with placeholder Supabase values.
The `hml-d6fc8d9-r1` tag is the first functional HML image set built with `STAGING_*`.

The `hml-d6fc8d9-r1` tag is the first functional HML Admin release candidate.
The `hml-d6fc8d9-r2` tag is the functional Shop Modelo release candidate with the correct `VITE_ADMIN_API_URL`.

## Routing note

The hostname `gestor-gastro-hml.umamitech.net.br` now serves the Portal do Lojista/Admin at `/`.
The Shop is not exposed on this hostname yet and can receive a dedicated hostname later if needed.
The Admin health check is available at `/api/health`, which is used for probes.

## Shop Modelo Hostname

The Shop Modelo is exposed separately at `shop-modelo-gestor-gastro-hml.umamitech.net.br`.
The tenant slug must match the hostname prefix: `shop-modelo-gestor-gastro-hml`.
On that hostname, `/api` proxies to the Admin service and `/` serves the Shop.
Cloudflare Access must protect the hostname before public exposure.

The Shop deployment remains on the last confirmed functional tag until the `hml-d6fc8d9-r2` image is verified and published; do not assume the newer tag exists without confirmation.

## Cloudflare Access

Cloudflare Access must protect `gestor-gastro-hml.umamitech.net.br` before the hostname is exposed publicly.
