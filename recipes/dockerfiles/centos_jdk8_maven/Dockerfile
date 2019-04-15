# Copyright (c) 2012-2019 Red Hat, Inc.
# All rights reserved. This program and the accompanying materials
# are made available under the terms of the Eclipse Public License v1.0
# which accompanies this distribution, and is available at
# http://www.eclipse.org/legal/epl-v10.html
# Contributors:
# Red Hat, Inc. - initial implementation

FROM quay.io/openshiftio/che-stack-base

# Install OpenJDK and Maven
RUN sudo yum upgrade -y -d 1 \
  && sudo yum install -y -d 1 \
    java-1.8.0-openjdk-devel \
    rh-maven35 \
  && sudo yum clean all \
  && sudo rm -rf /tmp/* /var/cache/yum \
  && cat /opt/rh/rh-maven33/enable >> /home/user/.bashrc
