# Configuração de Proxy Reverso com Nginx

Este guia descreve os passos para configurar um proxy reverso usando o servidor web Nginx. Um proxy reverso é útil para encaminhar solicitações de um nome de domínio para vários servidores ou portas em sua rede local. Aqui, usaremos o arquivo `/etc/hosts` para mapear nomes de domínio a endereços IP locais e configuraremos o Nginx para atuar como um proxy reverso para esses domínios.

## Passo 1: Adicionar Registros no `/etc/hosts`

Abra o arquivo `/etc/hosts` com um editor de texto, como o `sudo nano`:

```shell
sudo nano /etc/hosts
```

Adicione entradas para os domínios que deseja mapear para endereços IP locais. Por exemplo:

```plaintext
127.0.0.1       meu-dominio.local
127.0.0.1       outro-dominio.local
```

Salve o arquivo e saia do editor.

## Passo 2: Criar Blocos `server` no Arquivo de Configuração do Nginx

Acesse o diretório de configuração do Nginx:

```shell
cd reverse-proxy/sites-available
```

Crie um novo arquivo de configuração para o primeiro domínio, por exemplo, `meu-dominio.local`:

```shell
sudo nano meu-dominio.local
```

No arquivo de configuração, crie um bloco `server` que encaminhará solicitações para o domínio mapeado para uma porta ou servidor específico. Aqui está um exemplo:

```nginx
server {
    listen 80;
    server_name meu-dominio.local;

    location / {
        proxy_pass http://127.0.0.1:8080;
    }
}
```

Neste exemplo, todas as solicitações para `meu-dominio.local` serão encaminhadas para o endereço IP local `127.0.0.1` na porta `8080`. Salve o arquivo e saia do editor.

Pode ser necessário utilizar o ip da sua máquina na rede ao invés do ip local.

Repita o processo para cada domínio mapeado.

### Limpar cache do DNS no Chrome
- Acesse `chrome://net-internals/#dns` pelo chrome
- Clique no botão `Clear host cache`
