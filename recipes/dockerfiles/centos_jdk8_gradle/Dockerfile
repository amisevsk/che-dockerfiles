# Copyright (c) 2012-2019 Red Hat, Inc.
# All rights reserved. This program and the accompanying materials
# are made available under the terms of the Eclipse Public License v1.0
# which accompanies this distribution, and is available at
# http://www.eclipse.org/legal/epl-v10.html
# Contributors:
# Red Hat, Inc. - initial implementation

FROM quay.io/openshiftio/che-stack-base

ENV GRADLE_VERSION=5.3.1
ENV GRADLE_HOME=/opt/gradle

# Install OpenJDK
RUN sudo yum upgrade -y -d 1 \
  && sudo yum install -y -d 1 \
    java-1.8.0-openjdk-devel \
  && sudo yum clean all \
  && sudo rm -rf /tmp/* /var/cache/yum

# Install Gradle
RUN wget -q -P /tmp "https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip" \
  && sudo unzip -q -d /opt/gradle /tmp/gradle-${GRADLE_VERSION}-bin.zip \
  && sudo ln -s /opt/gradle/gradle-${GRADLE_VERSION}/bin/gradle /usr/bin/gradle \
  && sudo rm -rf /tmp/*