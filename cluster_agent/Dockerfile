FROM centos:latest

#add packages
RUN yum install -y java-1.8.0-openjdk-src.x86_64 which

# export agent port
EXPOSE 4445

# set working forlder
WORKDIR /root

# download and install jobscheduler agent
RUN curl -O https://download.sos-berlin.com/JobScheduler.1.10/jobscheduler_unix_universal_agent.1.10.0.tar.gz

# extract jobscheduler agent
RUN tar xfvz jobscheduler_unix_universal_agent.1.10.0.tar.gz

# execute the egent install script
CMD ["/root/jobscheduler_agent/bin/jobscheduler_agent.sh", "start_docker"]
