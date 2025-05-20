# Comandos para instalar Docker e Docker Compose no Linux

Executar os comandos de instalação e configuracao como Super Usuario

1.  Desinstalar versões antigas (opcional, mas recomendado)

    ```bash
    apt-get remove -y docker.io docker-doc docker-compose podman-docker containerd runc
    apt-get autoremove -y
    apt-get clean
    ```
2.  Configurar o repositório do Docker

    ```bash
    apt-get update
    apt-get install -y ca-certificates curl
    install -m 0755 -d /etc/apt/keyrings
    curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
    chmod a+r /etc/apt/keyrings/docker.asc
    echo \
      "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
      $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
      tee /etc/apt/sources.list.d/docker.list > /dev/null
    apt-get update
    ```
3.  Instalar Docker Engine e Docker Compose plugin

    ```bash
    apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
    ```
4.  Configurar permissões para executar Docker sem sudo

    ```bash
    usermod -aG docker $USER
    ```

    ```
    ---------------------------------------------------------------------
    IMPORTANTE: Para usar Docker sem sudo, FAÇA LOGOUT E LOGIN NOVAMENTE,
    ou reinicie, ou execute 'newgrp docker' em um novo terminal.
    ---------------------------------------------------------------------
    ```
5.  Verificar (após aplicar permissões)

    ```bash
    docker compose version
    ```

    Nota: Use `docker compose` (com espaço). O `docker-compose` (com hífen) é legado.
