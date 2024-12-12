FROM ubuntu:22.04

RUN apt update && apt install  openssh-server sudo -y
RUN apt remove --purge -y python3.10
RUN apt remove --purge -y python3
RUN apt autoremove -y
RUN mkdir /var/run/sshd
COPY ./id_rsa.pub /root/.ssh/authorized_keys

CMD ["/usr/sbin/sshd", "-D"]
