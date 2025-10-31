# Projeto de App: CineLibro 2.0 (Nome Provisório)

## 1. Visão Geral
**Objetivo:**  
Criar um app social multimídia onde usuários possam:
- Postar **vídeos longos** (mais de 24h)  
- Publicar **livros em PDF**  
- Participar de **chats temáticos** sobre filmes e séries  
- Receber recomendações personalizadas  
- Interagir com a comunidade de forma segura  

**Público-alvo:**  
Fãs de filmes, séries e literatura, criadores de conteúdo independentes e comunidades de entretenimento.

---

## 2. Funcionalidades do App

### 2.1 Usuário
- Cadastro/login: email, social login (Google/Apple/Facebook)  
- Perfil pessoal: avatar, bio, biblioteca de livros, vídeos favoritos  
- Histórico de visualização de vídeos e leitura de PDFs  
- Sistema de curtidas, comentários e compartilhamento  
- Notificações push e in-app (novos posts, respostas, recomendações)

### 2.2 Vídeos
- Upload de vídeos longos (>24h) com **resumable uploads**  
- Transcodificação automática para HLS/DASH  
- Player avançado:
  - Marcação de capítulos  
  - Velocidade de reprodução ajustável  
  - Busca por timestamp  
  - Comentários ligados a momentos específicos  
- Feed de vídeos com algoritmo de recomendação  
- Likes, comentários e compartilhamentos  

### 2.3 Livros (PDF)
- Upload de PDFs com metadados (título, autor, sinopse, tags)  
- Visualizador embutido (PDF.js ou nativo mobile)  
- Opção de download (se permitido pelo autor)  
- Sistema de versões (draft/publicado)  
- Comentários e avaliação por capítulo  
- Destaques e bookmarks  

### 2.4 Chats
- Dois chats públicos fixos: **Filmes** e **Séries**  
- Mensagens em tempo real (threads, reações, busca)  
- Notificações de novas mensagens  
- Moderação automática e manual  
- Salas privadas e grupos (futuro)  

### 2.5 Social & Engajamento
- Feed unificado de vídeos e livros  
- Sistema de tags e categorias  
- Sistema de trending posts  
- Recomendação baseada em IA  
- Rankings de usuários por engajamento  

### 2.6 Monetização
- Compras de livros pagos  
- Assinaturas premium (armazenamento extra, conteúdos exclusivos)  
- Doações para criadores  
- Créditos in-app  
- Estatísticas financeiras para autores e criadores  

### 2.7 Segurança e Controle
- Criptografia TLS 1.3  
- JWT + refresh tokens  
- Autenticação em 2 fatores (opcional)  
- Moderação de conteúdo com IA e humanos  
- Painel administrativo completo:
  - Gerenciar usuários, vídeos, livros e chats  
  - Relatórios de conteúdo, denúncias e estatísticas  
  - Logs de acesso e auditoria  
  - Controle de permissões por nível (admin, moderador, usuário)  
- Backup automático e versionamento de arquivos  
- Controle de upload: limites, quotas e filtros  

### 2.8 Painel Administrativo
- Gerenciamento completo do app e conteúdo  
- Moderação de usuários e posts  
- Estatísticas de uso (visualizações, uploads, engajamento)  
- Painel financeiro (vendas, assinaturas, doações)  
- Gestão de notificações  
- Ferramentas de relatório e exportação de dados  

### 2.9 Recursos IA
- Resumo automático de livros  
- Recomendações personalizadas (vídeos e livros)  
- Moderação automática de mensagens e uploads  
- Chatbot assistente (responde perguntas sobre livros e filmes)  
- Sugestão de tags para uploads  

### 2.10 Extras desejáveis
- Offline reading mode para PDFs  
- Download de vídeos (restrito ou premium)  
- Clipes e highlights automáticos de vídeos longos  
- Multi-idioma (Português/inglês inicialmente)  
- Estatísticas detalhadas para criadores  

---

## 3. Modelo de Dados

| Tabela | Campos principais |
|--------|-----------------|
| users | id, name, email, avatar, role, bio, created_at |
| videos | id, user_id, title, description, duration, hls_url, thumbnail, status, created_at |
| video_chapters | id, video_id, start_seconds, title |
| books | id, user_id, title, author_name, pdf_path, cover_path, description, is_paid, price, created_at |
| posts | id, owner_type, owner_id, type (video/book), caption, created_at |
| chats | id, name, description |
| chat_messages | id, chat_id, user_id, parent_id, content, metadata, created_at |
| reports | id, reporter_id, target_type, target_id, reason, status, created_at |
| transactions | id, user_id, target_id, amount, status, created_at |

---

## 4. Arquitetura Técnica

### Frontend
- Mobile: Flutter (Android + iOS)  
- Web: Next.js (React SSR)  
- Player de vídeo HLS/DASH  
- Visualizador PDF integrado  

### Backend
- Node.js + NestJS ou Django + DRF  
- REST + WebSocket (tempo real)  
- Filas de processamento (RabbitMQ/SQS)  
- Workers de transcodificação (FFmpeg)  

### Banco de Dados
- PostgreSQL (relacional)  
- Redis (cache + pub/sub)  
- Objet storage (S3/MinIO/Wasabi)  
- CDN (CloudFront/BunnyCDN)  

### Infraestrutura
- Docker + Kubernetes  
- TLS 1.3 obrigatório  
- Logs centralizados + monitoramento (Prometheus + Grafana)  
- Backup automático e versionamento de arquivos  

---

## 5. Endpoints Principais

**Autenticação:**  
- POST `/auth/register`  
- POST `/auth/login`  
- POST `/auth/refresh`  

**Vídeos:**  
- POST `/videos/upload/init`  
- PUT `/videos/upload/chunk`  
- GET `/videos/:id`  
- POST `/videos/:id/process`  

**Livros:**  
- POST `/books`  
- GET `/books/:id`  
- GET `/books/:id/download`  

**Chats:**  
- GET `/chats/:id/messages?cursor=`  
- POST `/chats/:id/messages` (WebSocket também)  
- GET `/chats/list`  

**Moderação:**  
- POST `/reports`  
- GET `/admin/reports`  
- POST `/admin/users/:id/ban`  

**Financeiro:**  
- POST `/transactions`  
- GET `/admin/transactions`  

---

## 6. Roadmap de Funcionalidades

**MVP**  
- Cadastro/login  
- Upload e streaming de vídeos longos  
- Upload e visualização de PDFs  
- Chats públicos  
- Feed unificado  
- Moderação básica  
- Painel administrativo  

**Fase 2**  
- Monetização (assinaturas, vendas de livros)  
- IA para recomendação e moderação  
- Notificações avançadas  
- Comentários em vídeos por timestamp  
- Rankings de usuários  
- Multi-idioma  

**Fase 3**  
- Clipes automáticos de vídeos  
- Chats privados e grupos  
- Estatísticas detalhadas para criadores  
- Offline reading/download  
- Integração com redes sociais  

---

## 7. Segurança
- TLS 1.3 em todas comunicações  
- JWT + refresh tokens  
- 2FA opcional  
- Rate limits em uploads e mensagens  
- Auditoria e logs completos  
- Painel de controle com permissões hierárquicas  
- Backup diário e versionamento de arquivos  

---

## 8. Design e UX
- Interface simples e intuitiva  
- Player de vídeo responsivo  
- Leitor PDF com navegação por capítulos  
- Feed limpo com cards de vídeo e livro  
- Chat em tempo real com threads e emojis  
- Dashboard administrativo com gráficos e filtros  

---

## 9. Requisitos Não-Funcionais
- Escalável horizontalmente  
- Alta disponibilidade (99,9%)  
- Latência mínima em streaming  
- Backup e disaster recovery  
- Conformidade LGPD/GDPR  
- Suporte a múltiplos idiomas  

---

## 10. Copy para App Store / Play Store
**Nome:** CineLibro  
**Descrição curta:** Poste vídeos longos, publique seus livros em PDF e converse sobre filmes e séries com a comunidade.  
**Pitch:** Crie, compartilhe e explore conteúdo sem limites. Streamings gigantes, PDFs interativos e chats para fãs — tudo em um só app.  

---

## 11. Checklist para Desenvolvimento

**Frontend:**  
- [ ] Tela de login/cadastro  
- [ ] Feed unificado  
- [ ] Upload resumable de vídeos  
- [ ] Player HLS/DASH com capítulos  
- [ ] Visualizador PDF  
- [ ] Chats em tempo real  
- [ ] Perfil de usuário e biblioteca  

**Backend:**  
- [ ] API REST + WebSocket  
- [ ] Workers de transcodificação  
- [ ] Moderação automática + manual  
- [ ] Painel administrativo  
- [ ] Sistema de monetização  
- [ ] Logs e auditoria  

**Infraestrutura:**  
- [ ] Docker + Kubernetes  
- [ ] TLS 1.3  
- [ ] Objet storage + CDN  
- [ ] Backup e disaster recovery  

---

## 12. Wireframes Textuais (telas principais)

**Tela Inicial:** Feed com cards de vídeo e livros  
**Tela Upload Vídeo:** Seleção arquivo, progresso, título, descrição, tags, capítulos  
**Player Vídeo:** HLS player, capítulos, comentários por timestamp  
**Biblioteca de Livros:** Lista de PDFs, filtros, leitura online  
**Leitor PDF:** Navegação por índice, bookmarks, download  
**Chats:** Lista mensagens, threads, reações, busca  
**Perfil Usuário:** Meus uploads, livros, configurações  
**Painel Admin:** Controle completo de usuários, conteúdo, estatísticas, finanças  

---


