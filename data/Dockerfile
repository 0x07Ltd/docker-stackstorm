FROM flyte/stackstorm-base
LABEL com.stackstorm.service.provides="data"

ADD ./st2.conf /etc/st2/st2.conf
ADD ./htpasswd /etc/st2/htpasswd
ADD ./id_rsa /home/stanley/.ssh/id_rsa
ADD ./id_rsa.pub /home/stanley/.ssh/id_rsa.pub
ADD ./known_hosts /home/stanley/.ssh/known_hosts
ADD ./id_rsa /root/.ssh/id_rsa
ADD ./id_rsa.pub /root/.ssh/id_rsa.pub
ADD ./known_hosts /root/.ssh/known_hosts

VOLUME /home/stanley/.ssh
VOLUME /root/.ssh

CMD st2-register-content --config-file /etc/st2/st2.conf --register-all
