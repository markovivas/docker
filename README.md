# 🐘 WordPress com Traefik e MariaDB

Este projeto utiliza Docker Compose para provisionar um ambiente de desenvolvimento completo para o WordPress, incluindo:

- **WordPress**: A plataforma de gerenciamento de conteúdo.
- **MariaDB**: O banco de dados para o WordPress.
- **Traefik**: Um proxy reverso moderno que gerencia o roteamento e a segurança.
- **HTTPS Automático**: Configuração para Let's Encrypt (para domínios públicos) e certificados autoassinados (para desenvolvimento local).

## ✨ Recursos

- **Proxy Reverso com Traefik**: Roteia o tráfego para o serviço do WordPress de forma segura.
- **Dashboard do Traefik**: Interface para monitorar e visualizar a configuração do Traefik.
- **HTTPS Automático**: Suporte integrado para certificados SSL via Let's Encrypt.
- **Persistência de Dados**: Os dados do WordPress, do banco de dados e dos certificados são salvos em volumes locais.
- **Redes Isoladas**: Serviços comunicam-se através de redes Docker dedicadas para maior segurança.

## 📋 Pré-requisitos

- **Docker**: Instruções de instalação
- **Docker Compose**: Instruções de instalação

## 🚀 Como Usar

1.  **Clone ou baixe este repositório.**

2.  **Configure as variáveis de ambiente.**
    É uma boa prática não colocar senhas e dados sensíveis diretamente no arquivo `docker-compose.yml`. Crie um arquivo chamado `.env` na mesma pasta e adicione o seguinte conteúdo, ajustando os valores conforme necessário:

    ```env
    # Domínio para o WordPress (ex: wordpress.meudominio.com ou intranet.local)
    WORDPRESS_DOMAIN=intranet.local

    # Credenciais do Banco de Dados
    DB_ROOT_PASSWORD=example_rootpass
    DB_NAME=wordpress
    DB_USER=wordpress
    DB_PASSWORD=example_dbpass

    # Email para o Let's Encrypt (use um email válido para domínios públicos)
    LETSENCRYPT_EMAIL=seu-email@example.com
    ```

3.  **Ajuste o `docker-compose.yml` (se necessário).**
    O arquivo `WordPress-com-Traefik.yml` está configurado para ler as variáveis do arquivo `.env`. Verifique se os nomes dos volumes e outras configurações atendem às suas necessidades.

4.  **Suba os contêineres.**
    Execute o seguinte comando no seu terminal:
    ```bash
    docker compose -f WordPress-com-Traefik.yml up -d
    ```

5.  **Configure seu DNS local (para domínios `.local`).**
    Se você estiver usando um domínio local como `intranet.local`, precisará editar o arquivo `hosts` do seu sistema para que ele aponte para o IP da máquina que está rodando o Docker.
    -   **Windows**: `C:\Windows\System32\drivers\etc\hosts`
    -   **Linux/macOS**: `/etc/hosts`

    Adicione a seguinte linha, substituindo `127.0.0.1` pelo IP do seu servidor Docker, se for diferente:
    ```
    127.0.0.1   intranet.local
    ```

6.  **Acesse os serviços.**
    -   **WordPress**: Abra seu navegador e acesse `https://intranet.local` (ou o domínio que você configurou).
    -   **Dashboard do Traefik**: Acesse `http://localhost:8080`.

## 📁 Estrutura de Diretórios

Após a execução, os seguintes diretórios serão criados para persistir os dados:

```
/
├── data/
│   ├── letsencrypt/  # Certificados SSL do Traefik
│   ├── mariadb/      # Dados do banco MariaDB
│   └── wordpress/    # Arquivos do WordPress (temas, plugins, uploads)
├── WordPress-com-Traefik.yml
└── .env
```

## 🔧 Serviços Definidos

- **traefik**: O proxy reverso.
- **mariadb**: O serviço de banco de dados.
- **wordpress**: O serviço do WordPress.

## ⚠️ Observações