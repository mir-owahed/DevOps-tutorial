Dockerfile
```
# Use the Eclipse Temurin OpenJDK 17 base image
FROM eclipse-temurin:17-jdk

# Ensure UTF-8 locale
ENV LANG=en_US.UTF-8 \
    LANGUAGE=en_US:en \
    LC_ALL=en_US.UTF-8

# (Optional) switch to a closer Debian mirror:
# RUN sed -i 's|http://deb.debian.org/debian|http://ftp.us.debian.org/debian|g' /etc/apt/sources.list

# Install Maven, Git, and other utilities in one layer
RUN apt-get update && \
    apt-get install -y --no-install-recommends --fix-missing \
      maven \
      git \
      curl \
      ca-certificates \
      gnupg2 \
      lsb-release \
      tar && \
    rm -rf /var/lib/apt/lists/*

# Install Docker CLI only (no daemon) by downloading the static binary
RUN curl -fsSL https://download.docker.com/linux/static/stable/x86_64/docker-25.0.0.tgz \
    | tar -xz --strip-components=1 -C /usr/local/bin docker/docker

# Create a docker group and a non-root 'jenkins' user for safer execution
RUN groupadd -g 1001 docker && \
    useradd -m -u 1001 -g docker jenkins

# Switch to non-root user
USER jenkins

# Set working directory
WORKDIR /workspace

# Default command: display Maven version (override as needed)
CMD ["mvn", "--version"]

```
