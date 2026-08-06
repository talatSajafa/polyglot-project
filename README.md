# 32-Bit (i686) Container Architecture & Debugging Log

An experimental 32-bit containerized stack (Node.js API, Python 3.11 Analytics, Nginx Proxy) built to resolve Docker Hub manifest deprecations and run on legacy `i686` hardware.

## 🛠️ Hardware Constraints & Workarounds

Running modern containers on native 32-bit (`i686`) systems triggered several low-level infrastructure failures:

- **Docker Hub Manifest Errors (`linux/386`):** Standard official images drop 32-bit builds. Pinned base layers strictly to `debian:bullseye-slim`.
- **NPM Memory Exhaustion:** Package resolution (`npm install`) hit RAM/swap limits on low-spec hardware.
- **Binary Mismatch (Exit Code 127):** Re-aligned execution paths explicitly to `/usr/local/bin`.

## 📂 Project Structure

- `node-api/`: Node.js API (Debian 32-bit base)
- `python-analytics/`: Python 3.11 microservice
- `nginx/`: Reverse proxy configuration
- `benchmark.txt`: Layer size and execution metric logs
- `docker-compose.yml`: Multi-container orchestrator

## 📊 Container Benchmarks

Metrics logged during execution testing:

| Service | Image | Size | Status |
| :--- | :--- | :--- | :--- |
| Node API | `polyglot-node-api` | 72.2 MB | Build Memory Bound |
| Python Analytics | `polyglot-python-analytics` | 135 MB | Verified (Py 3.11) |
| Nginx Proxy | `polyglot-nginx` | 160 MB | Operational |

## 🚀 Quick Run (Pre-built Binaries)

```bash
git clone [https://github.com/your-username/your-repo.git](https://github.com/your-username/your-repo.git)
cd your-repo
docker-compose up --build -d
```
# Status
- State: Archived Debug Log 
- Validation: Check benchmark.txt for raw logs
