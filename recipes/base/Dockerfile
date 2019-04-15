# Copyright (c) 2012-2019 Red Hat, Inc.
# All rights reserved. This program and the accompanying materials
# are made available under the terms of the Eclipse Public License v1.0
# which accompanies this distribution, and is available at
# http://www.eclipse.org/legal/epl-v10.html
# Contributors:
# Red Hat, Inc. - initial implementation
#
# This image is not meant to be used directly, but instead function as a base
# for Che 7 images.

FROM registry.centos.org/che-stacks/centos-stack-base

ARG OC_VERSION=3.9.38

# Install general dependencies
RUN sudo yum update -y -d 1 \
  && sudo yum install -y epel-release \
  && sudo yum install -y -d 1 \
    bzip2 \
    curl \
    gettext \
    git \
    tar \
    wget \
    nss_wrapper \
  && sudo wget -qO- "https://mirror.openshift.com/pub/openshift-v3/clients/${OC_VERSION}/linux/oc.tar.gz" \
    | sudo tar xvz -C /usr/local/bin \
  && curl -sL https://rpm.nodesource.com/setup_6.x | sudo -E bash - \
  && sudo yum install -y -d 1 \
    nodejs \
  && sudo yum remove -y epel-release \
  && sudo yum clean all \
  && sudo rm -rf /tmp/* /var/cache/yum

# The following lines are needed to set the correct locale after `yum update`
# c.f. https://github.com/CentOS/sig-cloud-instance-images/issues/71
RUN sudo localedef -i en_US -f UTF-8 C.UTF-8
ENV LANG="C.UTF-8"

# Generate passwd.template
RUN cat /etc/passwd | \
    sed s#user:x.*#user:x:\${USER_ID}:\${GROUP_ID}::\${HOME}:/bin/bash#g \
    > /home/user/passwd.template \
# Generate group.template
  && cat /etc/group | \
    sed s#root:x:0:#root:x:0:0,\${USER_ID}:#g \
    > /home/user/group.template

ENV HOME /home/user

# Overwride entrypoint
COPY ["./context/entrypoint.sh", "/home/user/entrypoint.sh"]
ENTRYPOINT ["/home/user/entrypoint.sh"]
CMD tail -f /dev/null

# Give write access to /home/user for users with an arbitrary UID
RUN sudo chgrp -R 0 /home/user \
  && sudo chmod -R g+rwX /home/user \
  && sudo chgrp -R 0 /etc/passwd \
  && sudo chmod -R g+rwX /etc/passwd \
  && sudo chgrp -R 0 /etc/group \
  && sudo chmod -R g+rwX /etc/group \
  && sudo mkdir -p /projects \
  && sudo chgrp -R 0 /projects \
  && sudo chmod -R g+rwX /projects \
  && sudo chgrp -R 0 /tmp \
  && sudo chmod -R g+rwX /tmp