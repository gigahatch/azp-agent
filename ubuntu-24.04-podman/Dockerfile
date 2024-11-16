FROM ubuntu:24.04
ENV TARGETARCH="linux-x64"
# Also can be "linux-arm", "linux-arm64".

RUN apt update
RUN apt upgrade -y
RUN apt install -y curl git jq libicu70 podman

WORKDIR /azp/

COPY ./start.sh ./
RUN chmod +x ./start.sh
COPY ./docker /usr/local/bin/
RUN chmod +x /usr/local/bin/docker
RUN touch /etc/containers/nodocker

# Create agent user and set up home directory
RUN useradd -m -d /home/agent agent
RUN chown -R agent:agent /azp /home/agent
RUN echo agent:10000:10000 > /etc/subuid; \
    echo agent:10000:10000 > /etc/subgid;

USER agent
# Another option is to run the agent as root.
# ENV AGENT_ALLOW_RUNASROOT="true"

ENTRYPOINT [ "./start.sh" ]