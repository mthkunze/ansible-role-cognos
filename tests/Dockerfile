FROM mkde/centos_cognos:1.0

# Install Ansible and dependences
RUN curl https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm -o epel-release-latest-7.noarch.rpm

RUN yum install -y epel-release-latest-7.noarch.rpm; \
yum install -y glibc.i686; \
yum install -y libstdc++; \
yum install -y nspr; \
yum install -y nss; \
yum install -y openmotif; \
rm -rf epel-release-latest-7.noarch.rpm

RUN yum install -y unzip tar gcc python-devel python-pip openssl-devel file python-setuptools libffi-devel libselinux-python python2-crypto git sudo

RUN pip install ansible; \
pip install --upgrade setuptools; \
sed -i -e 's/^\(Defaults\s*requiretty\)/#--- \1/'  /etc/sudoers; \
mkdir -p /etc/ansible/roles; \
echo -e '[local]\nlocalhost ansible_connection=local' > /etc/ansible/hosts

CMD ["/usr/sbin/init"]