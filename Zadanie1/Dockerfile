FROM ubuntu:22.04

RUN apt update && apt install -y \
    python3.10 \
    python3-pip \
    openjdk-8-jdk \
    curl \
    zip \
    unzip

RUN curl -sS https://get.sdkman.io | bash

RUN bash -c "source $HOME/.sdkman/bin/sdkman-init.sh && sdk install kotlin && sdk install gradle"

ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
ENV PATH="$PATH:/root/.sdkman/candidates/kotlin/current/bin:/root/.sdkman/candidates/gradle/current/bin"

WORKDIR /app

COPY src/build.gradle src/settings.gradle ./

RUN mkdir -p src/main/kotlin

COPY src/HelloWorld.kt src/main/kotlin/HelloWorld.kt

RUN gradle build --no-daemon --warning-mode all

CMD ["gradle", "run"]