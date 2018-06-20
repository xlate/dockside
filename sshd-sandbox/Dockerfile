FROM alpine:3.7

COPY ssh_host_* /etc/ssh/
COPY sshd-entry.sh /

RUN apk update && \
	apk add openssh-server && \
	mkdir -p /var/run/sshd && \
	adduser -D anonymous && \
	sed -i -re 's/^anonymous:[^:]+:/anonymous::/' /etc/passwd /etc/shadow && \
	printf "Match user anonymous\n    PermitEmptyPasswords yes\n    ForceCommand /sshd-entry.sh" >> /etc/ssh/sshd_config && \
	chmod +x /sshd-entry.sh

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
