FROM rust:1.73-bullseye

ENV TZ=America/Sao_Paulo
ENV DEBIAN_FRONTEND noninteractive

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update -yqq && \
  apt-get upgrade -y && \
  apt-get install -y --no-install-recommends \
  git \
  wget \
  curl \
  unzip \
  nano \
  vim \
  zsh

RUN groupadd -g 1000 dev && \
  useradd -m -u 1000 -g dev -s $(which zsh) dev

COPY . /app

WORKDIR /app

USER dev:dev

RUN curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh | sh; zsh && \
  git clone https://github.com/zsh-users/zsh-autosuggestions.git /home/dev/.oh-my-zsh/plugins/zsh-autosuggestions && \
  git clone https://github.com/zsh-users/zsh-syntax-highlighting.git /home/dev/.oh-my-zsh/plugins/zsh-syntax-highlighting

COPY .zshrc /home/dev/.zshrc

EXPOSE 8080

CMD ["tail", "-f", "/dev/null"]
