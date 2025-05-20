# Comandos para instalar Docker e Docker Compose no Linux (Debian/Ubuntu)

Siga os passos abaixo como superusuário (por exemplo, prefixando os comandos com `sudo` ou logado como root).

## 1. Remover versões antigas do Docker (Opcional)

Para evitar conflitos, é recomendável remover instalações antigas do Docker:
```bash
apt-get remove docker docker-engine docker.io containerd runc
apt-get purge docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-ce-rootless-extras -y
rm -rf /var/lib/docker
rm -rf /var/lib/containerd
```

## 2. Preparar o sistema e instalar dependências comuns

Atualize o índice de pacotes e instale as dependências necessárias:
```bash
apt-get update
apt-get install -y ca-certificates curl gnupg lsb-release
```

## 3. Configurar o repositório do Docker

Este passo difere ligeiramente entre Debian e Ubuntu. Siga as instruções para a sua distribuição.

### Para Debian

a. Adicionar a chave GPG oficial do Docker para Debian:
```bash
install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg
chmod a+r /etc/apt/keyrings/docker.gpg
```

b. Adicionar o repositório do Docker para Debian:
```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### Para Ubuntu

a. Adicionar a chave GPG oficial do Docker para Ubuntu:
```bash
install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg
chmod a+r /etc/apt/keyrings/docker.gpg
```

b. Adicionar o repositório do Docker para Ubuntu:
```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null
```

## 4. Instalar Docker Engine e Plugins

Após configurar o repositório para sua distribuição, atualize o índice de pacotes novamente e instale o Docker:
```bash
apt-get update
apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

## 5. Configurar permissões para executar Docker sem `sudo` (Pós-instalação)

Para executar comandos Docker sem `sudo`, adicione seu usuário ao grupo `docker`:
```bash
usermod -aG docker $USER
```
**IMPORTANTE:** Para que esta alteração tenha efeito, você **DEVE** fazer logout e login novamente na sua sessão. Alternativas incluem reiniciar o sistema ou executar `newgrp docker` em um novo terminal (esta última afeta apenas a sessão do terminal atual).

## 6. Verificar a instalação

Após aplicar as permissões e relogar (ou reiniciar/usar `newgrp docker`), verifique se a instalação foi bem-sucedida:
```bash
docker --version
docker compose version
```
Dica: Use `docker compose` (com espaço). O comando `docker-compose` (com hífen) refere-se a uma versão mais antiga e legada, substituída pelo plugin `docker-compose-plugin`.
