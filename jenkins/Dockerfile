FROM jenkins/jenkins:lts


USER root


# Install dependencies
RUN apt-get update && \
    apt-get install -y \
    wget \
    unzip \
    gnupg \
    curl \
    docker.io \
    && rm -rf /var/lib/apt/lists/*



# -----------------------------
# Install Trivy
# -----------------------------

RUN wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key \
| gpg --dearmor \
-o /usr/share/keyrings/trivy.gpg


RUN echo \
"deb [signed-by=/usr/share/keyrings/trivy.gpg] \
https://aquasecurity.github.io/trivy-repo/deb generic main" \
> /etc/apt/sources.list.d/trivy.list


RUN apt-get update && \
    apt-get install -y trivy && \
    rm -rf /var/lib/apt/lists/*



# -----------------------------
# Install SonarQube Scanner
# -----------------------------

RUN wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-7.2.0.5079-linux-x64.zip \
&& unzip sonar-scanner-cli-7.2.0.5079-linux-x64.zip -d /opt \
&& mv /opt/sonar-scanner-7.2.0.5079-linux-x64 /opt/sonar-scanner \
&& ln -s /opt/sonar-scanner/bin/sonar-scanner /usr/local/bin/sonar-scanner \
&& rm sonar-scanner-cli-7.2.0.5079-linux-x64.zip



# Docker permissions

RUN groupadd -f docker && \
    usermod -aG docker jenkins


RUN chown -R jenkins:jenkins /var/jenkins_home



USER jenkins
