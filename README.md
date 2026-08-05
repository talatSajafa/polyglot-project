# Polyglot 32-Bit Microservice Architecture (Archived / Legacy Research)

An experimental 32-bit (i686) containerized architecture featuring a Node API, Python 3.11 Analytics service, and Nginx Reverse Proxy. Engineered to test physical legacy hardware constraints and resolve 32-bit Docker Hub manifest deprecations.

---

## 🏗️ Technical Breakdown & Hardware Constraints

Standard modern container environments target 64-bit (`amd64`/`arm64`) architectures. Running this stack on native 32-bit `i686` hardware hit severe infrastructure barriers:

1. **Manifest Mismatch Failures (`no matching manifest`):** Modern base images no longer publish `linux/386` tags on Docker Hub. Baseline dependencies were bound to `debian:bullseye-slim` to allow native execution.
2. **Memory & Runtime Limitations:** Node runtime dependencies hit memory allocation locks during package resolution (`npm install` failure loops). Python runtime was successfully pinned to `Python 3.11`.
3. **Execution Verification:** Full functional state and original container layer sizes were logged and validated in `benchmark.txt`.

---

## 📂 Repository Structure

* `node-api/` : Node.js API service targeting 32-bit Debian environment
* `python-analytics/` : Python 3.11 microservice container
* `nginx/` : Nginx reverse proxy configuration
* `benchmark.txt` : Original execution metrics & layer size validation log
* `docker-compose.yml` : Multi-container orchestrator file
* `README.md` : Technical documentation & post-mortem analysis

---

## 📊 Recorded Benchmark Metrics

Historical snapshot verified via `benchmark.txt` prior to low-spec hardware locks:

| Service Name | Docker Image Name | Size | Execution State |
| :--- | :--- | :--- | :--- |
| Node API | polygot-project_node-api | 72.2 MB | Build Memory Bound |
| Python Analytics | polygot-project_python-analytics | 135 MB | Verified (Py 3.11) |
| Nginx Proxy | polygot-project_nginx | 160 MB | Operational |

---

## ⚠️ Known Hardware & Build Issues

| Issue / Error | Root Cause | Current Status / Mitigation |
| :--- | :--- | :--- |
| `no matching manifest for linux/386` | Docker Hub dropped 32-bit tags for modern Node images. | Resolved via `debian:bullseye-slim` base layer. |
| **Exit Code 127** | Architecture binary path mismatch in 32-bit userland. | Paths re-aligned to `/usr/local` binaries. |
| **Exit Code 100** | APT package index update timeouts on minimal Debian. | Resolved via package source list updates. |
| `npm install` Hang / Stalls | RAM & swap exhaustion during dependency tree resolution on i686. | Archived; requires pre-built binary mounting. |

---

## 📌 Project Status

* Status: Archived Research / Post-Mortem Documentation
* Validation Source: `benchmark.txt`
* Last Updated: August 5, 2026
