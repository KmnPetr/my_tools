FROM eclipse-temurin:21-jdk-alpine

ARG USER_ID=1000
ARG GROUP_ID=1000
ARG DOCKER_GROUP_ID=984

RUN apk add --no-cache \
    bash \
    ca-certificates \
    curl \
    docker-cli \
    docker-cli-compose \
    fontconfig \
    git \
    maven \
    nodejs \
    npm \
    openssh-client \
    ttf-dejavu

RUN addgroup -g ${DOCKER_GROUP_ID} docker \
 && addgroup -g ${GROUP_ID} petr \
 && adduser -D -u ${USER_ID} -G petr petr \
 && addgroup petr docker

RUN mkdir -p /usr/share/jenkins \
 && curl -fsSL https://get.jenkins.io/war-stable/latest/jenkins.war -o /usr/share/jenkins/jenkins.war \
 && chown -R petr:petr /usr/share/jenkins

USER petr
ENV JENKINS_HOME=/home/petr/.jenkins

EXPOSE 8080
EXPOSE 50000

CMD ["java", "-jar", "/usr/share/jenkins/jenkins.war"]
