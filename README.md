# WordPress com Traefik

Este projeto utiliza Docker Compose para criar um ambiente WordPress com proxy reverso Traefik, banco de dados MariaDB e HTTPS automático via Let's Encrypt.

## Arquivos

- **WordPress-com-Traefik.yml**: Arquivo principal do Docker Compose que define os serviços e redes.

## Serviços

### Traefik (Proxy Reverso)
- Imagem: `traefik:v2.10`
- Dashboard: Porta 8080
- HTTPS automático via Let's Encrypt
- Redireciona tráfego para o WordPress

### Banco de Dados (MariaDB)
- Imagem: `mariadb:latest`
- Usuário: `wordpress`
- Senha: `example_dbpass`
- Database: `wordpress`

### WordPress
- Imagem: `wordpress:latest`
- Conectado ao banco MariaDB
- Persistência de dados em `./data/wordpress`
- Acessível via Traefik em `https://intranet.local`

## Redes
- `traefik_network`: Rede para o Traefik e WordPress
- `wordpress_network`: Rede para o WordPress e banco de dados

## Como usar
1. Edite o arquivo `WordPress-com-Traefik.yml` conforme necessário (domínio, senhas, etc).
2. Execute:
	```bash
	docker compose -f WordPress-com-Traefik.yml up -d
	```
3. Acesse o dashboard do Traefik em `http://localhost:8080`.
4. Acesse o WordPress em `https://intranet.local` (configure o DNS/local para apontar para seu servidor).

## Volumes
- `./data/letsencrypt`: Armazena certificados gerados pelo Traefik
- `./data/mariadb`: Dados do banco MariaDB
- `./data/wordpress`: Dados do WordPress

## Observações
- Certifique-se de que o domínio `intranet.local` aponte para o IP do servidor Docker.
- O Traefik gerencia os certificados SSL automaticamente.