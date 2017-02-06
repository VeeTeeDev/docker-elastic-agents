FROM ...

# install whatever packages you need, in addition to the JRE, and git
# apt-get install openjdk-8-jre-headless git
# yum install java-1.8.0-openjdk-headless git

# download tini to ensure that an init process exists
ADD https://github.com/krallin/tini/releases/download/v0.14.0/tini /tini
RUN chmod +x /tini
ENTRYPOINT ["/tini", "--"]

# ensure that the container logs on stdout
ADD log4j.properties /var/lib/go-agent/log4j.properties
ADD log4j.properties /var/lib/go-agent/go-agent-log4j.properties

ADD https://github.com/ketan/gocd-golang-bootstrapper/releases/download/1.0/go-bootstrapper-1.0.linux.amd64 /go/go-agent
RUN chmod 755 /go/go-agent

# Add a user to run the go agent
RUN adduser go go -h /go -S -D

# Run the bootstrapper as the `go` user
USER go
CMD /go/go-agent
