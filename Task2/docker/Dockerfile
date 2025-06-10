FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

# Обновление и установка системных зависимостей
# Проверка версии `python3 --version`
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        curl \
        wget \
        ca-certificates \
        python3 \
        python3-pip \
        python3-setuptools \
        python3-wheel \
        python3-dev \
        build-essential \
        gnupg2 \
        apt-transport-https \
        conntrack \
        socat \
        iproute2 \
        iptables \
        # для minikube/kubectl
        sudo \
        # для корректной работы некоторых утилит
        bash \
    && rm -rf /var/lib/apt/lists/*

# Установка Minikube
# Проверка версии `minikube version`
RUN curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && \
    install minikube-linux-amd64 /usr/local/bin/minikube && \
    rm minikube-linux-amd64

# Установка kubectl
# Проверка версии `kubectl version --client`
RUN curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl" && \
    install -m 0755 kubectl /usr/local/bin/kubectl && \
    rm kubectl

# Установка Locust через pip \
# Проверка версии `locust --version`
RUN pip3 install --no-cache-dir locust

# Установка pip последней версии (опционально) \
# Проверка версии `pip --version`
RUN pip3 install --upgrade pip

# Создание рабочего каталога
WORKDIR /workspace

# Открываем порты для Locust (8089 - web, 5557 - master/worker)
EXPOSE 8089 5557

# По умолчанию запуск интерактивного shell
CMD ["/bin/bash"]


#Сборка и запуск docker image
#docker build -t scaletest-kuber .
#docker run -it --rm --privileged -p 8089:8089 -p 5557:5557 --name scaletest-kuber scaletest-kuber

#Проверка версий ПО
#minikube version
#kubectl version --client
#python3 --version
#pip --version
#locust --version
