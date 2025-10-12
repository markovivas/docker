# 🚀 Coleção de Arquivos Docker Compose

Este repositório contém uma coleção de arquivos `docker-compose.yaml` para provisionar rapidamente diversos serviços auto-hospedados (self-hosted). Cada arquivo é independente e foi projetado para uma aplicação específica.

## 📋 Pré-requisitos

Antes de começar, certifique-se de ter o Docker e o Docker Compose instalados em sua máquina.

- **Instalação do Docker**
- **Instalação do Docker Compose**

## ⚙️ Serviços Disponíveis

Abaixo está a lista dos serviços configurados nos arquivos `.yaml` deste repositório.

---

### 1. Nginx Proxy Manager

Este serviço provisiona o **Nginx Proxy Manager**, uma interface gráfica para gerenciar hosts de proxy reverso e certificados SSL/TLS de forma simplificada.

- **Arquivo**: `81-docker-compose-nginx-proxy-manager.yaml`
- **Acesso à Interface**: `http://<seu-ip>:81`
- **Portas Expostas**: `80` (HTTP), `443` (HTTPS), `81` (Admin).
- **Volumes**: Os dados e certificados são persistidos na pasta `./data` e `./letsencrypt`.
- **Credenciais Padrão**:
  - **Email**: `admin@example.com`
  - **Senha**: `changeme`

**Como executar:**
```bash
docker compose -f 81-docker-compose-nginx-proxy-manager.yaml up -d
```

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Painel de Serviços</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <style>
    :root {
      --primary-color: #4361ee;
      --secondary-color: #3a0ca3;
      --accent-color: #4cc9f0;
      --light-color: #f8f9fa;
      --dark-color: #212529;
      --success-color: #4bb543;
      --card-bg: #ffffff;
      --shadow: 0 10px 20px rgba(0,0,0,0.1);
      --transition: all 0.3s ease;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }

    body {
      background: linear-gradient(135deg, #f0f2f5 0%, #e6e9f0 100%);
      min-height: 100vh;
      padding: 40px 20px;
      text-align: center;
      color: var(--dark-color);
    }

    .header {
      margin-bottom: 40px;
      position: relative;
    }

    h1 {
      font-size: 2.5rem;
      margin-bottom: 10px;
      color: var(--secondary-color);
      position: relative;
      display: inline-block;
    }

    h1:after {
      content: '';
      position: absolute;
      bottom: -10px;
      left: 50%;
      transform: translateX(-50%);
      width: 100px;
      height: 4px;
      background: linear-gradient(to right, var(--primary-color), var(--accent-color));
      border-radius: 2px;
    }

    .subtitle {
      font-size: 1.1rem;
      color: #666;
      max-width: 600px;
      margin: 20px auto 0;
      line-height: 1.6;
    }

    .container {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 25px;
      max-width: 1200px;
      margin: 0 auto;
    }

    .card {
      background-color: var(--card-bg);
      padding: 30px 20px;
      border-radius: 15px;
      box-shadow: var(--shadow);
      transition: var(--transition);
      position: relative;
      overflow: hidden;
      display: flex;
      flex-direction: column;
      align-items: center;
      text-align: center;
    }

    .card:before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 5px;
      background: linear-gradient(to right, var(--primary-color), var(--accent-color));
    }

    .card:hover {
      transform: translateY(-10px);
      box-shadow: 0 15px 30px rgba(0,0,0,0.15);
    }

    .card-icon {
      width: 70px;
      height: 70px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      margin-bottom: 20px;
      background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
      color: white;
      font-size: 1.8rem;
      box-shadow: 0 5px 15px rgba(67, 97, 238, 0.3);
    }

    .card a {
      text-decoration: none;
      color: var(--dark-color);
      font-size: 1.4rem;
      font-weight: 600;
      margin-bottom: 10px;
      transition: var(--transition);
    }

    .card a:hover {
      color: var(--primary-color);
    }

    .description {
      color: #666;
      font-size: 0.95rem;
      line-height: 1.5;
      margin-bottom: 15px;
    }

    .card-footer {
      margin-top: auto;
      width: 100%;
    }

    .status {
      display: inline-block;
      padding: 5px 12px;
      border-radius: 20px;
      font-size: 0.8rem;
      font-weight: 600;
      background-color: rgba(75, 181, 67, 0.1);
      color: var(--success-color);
    }

    .footer {
      margin-top: 60px;
      color: #777;
      font-size: 0.9rem;
    }

    @media (max-width: 768px) {
      h1 {
        font-size: 2rem;
      }
      
      .container {
        grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
        gap: 20px;
      }
    }

    @media (max-width: 480px) {
      body {
        padding: 20px 15px;
      }
      
      h1 {
        font-size: 1.8rem;
      }
      
      .subtitle {
        fontSize: 1rem;
      }
    }
  </style>
</head>
<body>

  <div class="header">
    <h1>🌐 Painel de Serviços Locais</h1>
    <p class="subtitle">Acesse todos os seus serviços hospedados localmente em um só lugar</p>
  </div>

  <div class="container">
    <div class="card">
      <div class="card-icon">
        <i class="fas fa-server"></i>
      </div>
      <a href="http://192.168.2.100:81/settings" target="_blank">Nginx Proxy Manager</a>
      <div class="description">Gerenciador de Proxies Reversos para configurar domínios e certificados SSL</div>
      <div class="card-footer">
        <span class="status">Online</span>
      </div>
    </div>

    <div class="card">
      <div class="card-icon">
        <i class="fab fa-wordpress"></i>
      </div>
      <a href="http://192.168.2.100:8081" target="_blank">WordPress</a>
      <div class="description">Sistema de gerenciamento de conteúdo para criação de blogs e sites</div>
      <div class="card-footer">
        <span class="status">Online</span>
      </div>
    </div>

    <div class="card">
      <div class="card-icon">
        <i class="fab fa-youtube"></i>
      </div>
      <a href="http://192.168.2.100:8082" target="_blank">MeTube</a>
      <div class="description">Baixe vídeos de diversas plataformas diretamente pelo navegador</div>
      <div class="card-footer">
        <span class="status">Online</span>
      </div>
    </div>

    <div class="card">
      <div class="card-icon">
        <i class="fas fa-cloud"></i>
      </div>
      <a href="http://192.168.2.100:8083" target="_blank">Nextcloud</a>
      <div class="description">Solução de nuvem pessoal para armazenamento e colaboração</div>
      <div class="card-footer">
        <span class="status">Online</span>
      </div>
    </div>

    <div class="card">
      <div class="card-icon">
        <i class="fas fa-file-alt"></i>
      </div>
      <a href="http://192.168.2.100:8084" target="_blank">OnlyOffice</a>
      <div class="description">Suite de escritório online para edição de documentos em tempo real</div>
      <div class="card-footer">
        <span class="status">Online</span>
      </div>
    </div>

    <div class="card">
      <div class="card-icon">
        <i class="fas fa-music"></i>
      </div>
      <a href="http://192.168.2.100:8085" target="_blank">Navidrome</a>
      <div class="description">Servidor de música pessoal compatível com aplicativos Subsonic</div>
      <div class="card-footer">
        <span class="status">Online</span>
      </div>
    </div>

    <!-- NOVO CARD DO GITEA -->
    <div class="card">
      <div class="card-icon">
        <i class="fab fa-git-alt"></i>
      </div>
      <a href="http://192.168.2.100:8086" target="_blank">Gitea</a>
      <div class="description">Serviço de Git auto-hospedado para versionamento de código e colaboração</div>
      <div class="card-footer">
        <span class="status">Online</span>
      </div>
    </div>

    <div class="card">
      <div class="card-icon">
        <i class="fas fa-cube"></i>
      </div>
      <a href="http://192.168.2.100:25565" target="_blank">Minecraft Server</a>
      <div class="description">Servidor de Minecraft para jogar com amigos na sua rede local</div>
      <div class="card-footer">
        <span class="status">Online</span>
      </div>
    </div>
  </div>

  <div class="footer">
    <p>Painel de Serviços Locais • Atualizado em <span id="current-date"></span></p>
  </div>

  <script>
    // Adiciona a data atual no rodapé
    document.getElementById('current-date').textContent = new Date().toLocaleDateString('pt-BR');
    
    // Adiciona efeito de clique nos cards
    document.querySelectorAll('.card').forEach(card => {
      card.addEventListener('click', function(e) {
        if (e.target.tagName !== 'A') {
          const link = this.querySelector('a');
          if (link) {
            window.open(link.href, '_blank');
          }
        }
      });
    });
  </script>

</body>
</html>
```

---

### 2. WordPress (Simples)

Uma configuração básica do **WordPress** com um banco de dados **MariaDB**. Ideal para desenvolvimento rápido ou para ser usado atrás de um proxy reverso existente (como o Nginx Proxy Manager).

- **Arquivo**: `8081-docker-compose-wordpress.yaml`
- **Acesso ao WordPress**: `http://<seu-ip>:8081`
- **Portas Expostas**: `8081` (WordPress).
- **Volumes**: Os dados do WordPress e do MariaDB são persistidos em `./data/wordpress` e `./data/mariadb`.

**Como executar:**
```bash
docker compose -f 8081-docker-compose-wordpress.yaml up -d
```

> **⚠️ Atenção**: As senhas do banco de dados estão definidas diretamente no arquivo. Para ambientes de produção, é recomendado usar variáveis de ambiente ou secrets do Docker.

---

### 3. Gitea (Servidor Git)

Provisiona o **Gitea**, um serviço Git auto-hospedado, leve e de código aberto, similar ao GitHub ou GitLab. Ele utiliza um banco de dados **MySQL**.

- **Arquivo**: `8086-docker-compose-gitea.yaml`
- **Acesso ao Gitea**: `http://<seu-ip>:8086`
- **Portas Expostas**: `8086` (HTTP), `222` (SSH).
- **Volumes**: Os dados do Gitea e do MySQL são persistidos na pasta `./gitea`.

**Como executar:**
```bash
docker compose -f 8086-docker-compose-gitea.yaml up -d
```

> **⚠️ Atenção**: As senhas do banco de dados estão definidas diretamente no arquivo. Para ambientes de produção, é recomendado usar variáveis de ambiente ou secrets do Docker.