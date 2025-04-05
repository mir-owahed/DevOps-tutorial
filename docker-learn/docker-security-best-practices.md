# 🛡️ Docker Security Best Practices

A step-by-step guide to building secure, production-ready Docker images and containers.

---

## 🧱 1. Use Minimal and Trusted Base Images

- Prefer official, minimal images like:
  - `alpine`, `slim`, `distroless`, `eclipse-temurin:jre-alpine`
- Avoid using the `latest` tag:
  ```dockerfile
  FROM python:3.10-slim
  ```

---

## 📁 2. Use a `.dockerignore` File

Prevent sensitive or unnecessary files from being added to your image.

Example `.dockerignore`:

```
.git
__pycache__/
node_modules/
.env
*.pem
id_rsa*
target/
```

---

## 🏗️ 3. Use Multi-Stage Builds

Separate build tools from final runtime.

```dockerfile
FROM maven:3.8.3 AS builder
# Build your app here

FROM eclipse-temurin:17-jre-alpine
# Only copy the final artifact
```

---

## 👤 4. Avoid Running as Root

```dockerfile
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
USER appuser
```

---

## 🔐 5. Keep Secrets Out of Images

- Never copy `.env`, SSH keys, or config files into images.
- Use:
  - Docker secrets (Swarm)
  - AWS Secrets Manager
  - GitHub Actions Secrets

---

## 🧪 6. Scan Images for Vulnerabilities

- Use tools like:
  - `docker scan`
  - `trivy` (recommended)
  - `grype`

```bash
trivy image my-app:latest
```

---

## 🔒 7. Use Docker Security Flags

Limit container permissions:

```bash
docker run \
  --read-only \
  --cap-drop ALL \
  my-app
```

---

## 🌐 8. Restrict Network Access

- Use user-defined networks.
- Avoid unnecessary exposed ports.
- Prefer `--network=bridge` only if needed.

---

## 📂 9. Use `COPY` Instead of `ADD`

```dockerfile
COPY app.jar /app/
```

Use `ADD` only for TAR archives or remote URLs.

---

## 📉 10. Keep Images Small

- Use multi-stage builds
- Use `alpine` or `distroless`
- Remove unnecessary build tools/files

---

## 🧹 11. Clean Up Package Caches

```dockerfile
RUN apt-get update && apt-get install -y curl \
  && rm -rf /var/lib/apt/lists/*
```

---

## 📜 12. Use Immutable Image Tags

Avoid `:latest` in CI/CD.

```yaml
image: my-app:1.2.3
```

---

## 🔏 13. Sign and Verify Images

Enable Docker Content Trust:

```bash
export DOCKER_CONTENT_TRUST=1
docker push my-app
```

---

## 🛡️ 14. Enable Runtime Protection

- Use:
  - [Falco](https://falco.org/)
  - AppArmor
  - Seccomp

---

## ⚙️ 15. Secure Docker Daemon

- Don’t expose the Docker socket
- Use TLS for remote access
- Use `--icc=false` to restrict container communication

---

## ✅ Summary

| Area              | Best Practice                                      |
|-------------------|----------------------------------------------------|
| Base Image        | Use minimal trusted images                         |
| User Permissions  | Don’t run as root                                  |
| Secrets           | Use external secret managers                       |
| Image Size        | Use multi-stage builds                             |
| Network           | Limit exposed ports and use custom networks        |
| Security Flags    | Drop capabilities, use read-only FS                |
| Runtime Scanning  | Use Trivy, Docker Scan, or Grype                   |

---

## 📌 Want More?

- [Docker Official Security Docs](https://docs.docker.com/engine/security/)
- [OWASP Docker Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Docker_Security_Cheat_Sheet.html)

