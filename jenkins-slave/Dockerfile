
FROM ubuntu:xenial
RUN apt update && apt install -y curl  openssh-server default-jre vim  apt-transport-https ca-certificates curl gnupg-agent software-properties-common
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - && apt-key fingerprint 0EBFCD88 && add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu xenial stable"
RUN apt update && apt install -y docker-ce docker-ce-cli containerd.io
RUN mkdir -p /root/.ssh/
RUN echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCqpH0udEQwwaZj4Q64exPx0qd3CgOXJzOyyrUkNgyt77msDXYdCyNUlJ10KthaAbuw5iS2nT0JkOe5/ad+tV4eHBikp4IXy4XaKoWX51N9/PBUtLfSYRcqoxZP+90wjIDt7RUNK46o5aygFk+n1fxG8Zwi+NiOzpU4yd40mu2zDwhCUpedwAAWupF4ExykwPoeA30uySPQIxF34DaCnqfA3uIS8NLArs+w/IVlh+YHZho/2mEXa3iPoRR3WyYNoklCqMwdt22wf0FjaAyfnZN54iQ+w9Y/41h/6QJP01d8fDUIPwCS3zWeHhN8ngUM9Y7LpoRUvlbCUhgo7mky/KRX" >> /root/.ssh/authorized_keys
RUN chmod 700 /root/.ssh/authorized_keys
COPY start.sh /opt/start.sh
RUN chmod +x /opt/start.sh
CMD ["/opt/start.sh"]
