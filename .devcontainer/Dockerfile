FROM ubuntu:22.04
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y pipx cmake wget gcc g++ ruby git
RUN pipx ensurepath && pipx install gcovr
RUN gem install ceedling --version 0.31.1
