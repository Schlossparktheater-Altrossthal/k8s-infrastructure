# Schlossparktheater Altroßthal — K8s Infrastructure

GitOps repository for all Kubernetes workloads of Schlossparktheater Altroßthal.
Managed via ArgoCD on the shared K3s cluster.

## Cluster

| Node | Role | IP |
|------|------|----|
| vmd116756 (LimitlessGreen) | control-plane, edge | 82.208.22.191 |
| vmd179361 (Sommertheater) | worker | 38.242.238.59 |

## Services

### Native in K8s (migrated/planned)
| Service | Domain | Status |
|---------|--------|--------|
| Website | sommertheater-altrossthal.de | planned |
| Immich | photos.sommertheater-altrossthal.de | planned |
| RustFS | console.sommertheater-altrossthal.de | planned |

### Stays in Docker Compose (node 2)
| Service | Reason |
|---------|--------|
| Mailu | Complex mail stack, not K8s-ready |
| Nextcloud AIO | Designed for Docker AIO |
| Vaultwarden | Theater-specific instance |
| Authentik | SSO, evaluate later |

## Traffic Flow

```
Internet → DNS (sommertheater-altrossthal.de) → 82.208.22.191 (Node 1 Traefik)
                                                → docker-backends (Node 2 services via WireGuard)
```
