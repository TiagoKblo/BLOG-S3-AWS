# Blog Estático com Next.js + S3 + CloudFront

Este projeto é uma adaptação do template [`blog-starter`](https://github.com/vercel/next.js/tree/canary/examples/blog-starter) da Vercel. Utiliza o framework **Next.js** para gerar conteúdo estático hospedado na **AWS S3**, com distribuição via **Amazon CloudFront**, DNS gerenciado via **Route 53**, e domínio gratuito registrado na **Freenom**.

---

## 👨‍🏫 Informações Acadêmicas

- **Curso:** 6º Semestre – FATEC Itapira  
- **Professor:** Matheus Fuini  
- **Matéria:** Computação em Nuvem 2  
- **Integrantes do Grupo:**
  - Bruno Gomes de Oliveira  
  - Carlos Eduardo Nicioli  
  - Luis Felipe Salvarani  
  - Rafael Henrique de Oliveira  
  - Tiago Henrique de Moraes  

---

## 📦 Tecnologias utilizadas

- Next.js (Static HTML Export)
- AWS S3 (Website Hosting)
- AWS CloudFront (CDN)
- AWS Route 53 (DNS)
- Freenom (Domínio gratuito)
- IaC (Infrastructure as Code) com CloudFormation (template opcional)

---

## 🚀 Como foi feito o deploy

### 1. Clonagem e build do projeto

```bash
git clone https://github.com/vercel/next.js
cd next.js/examples/blog-starter
npm install
npm run build
npx next export
```

O comando `npx next export` gera a pasta `out/` com os arquivos HTML estáticos.

---

### 2. Upload para o S3

- Criado bucket com nome **exato** do domínio: `meusitefatec.tk`
- Ativado static website hosting em `index.html`
- Realizado upload da pasta `out/` (conteúdo direto)

---

### 3. Distribuição com CloudFront

- Criada uma distribuição CloudFront apontando para o bucket S3 como origem
- Configurada política de acesso público somente via CloudFront
- Adicionado comportamento de erro para redirecionar erros 403/404 para `index.html`

---

### 4. Configuração do domínio (Freenom + Route 53)

- Domínio gratuito registrado via [Freenom](https://www.freenom.com/)
- Zona hospedada criada no Route 53
- Nameservers do Route 53 copiados para o painel Freenom
- Criado registro `A` com alias para o **CloudFront**

---

## 🌐 Acesso ao site

📍 **Link do site em produção:**  
[https://meusitefatec.tk](https://meusitefatec.tk)

---

## 📁 Organização do Repositório

```
📁 nextjs-blog-s3-cloudfront
 ┣ 📁 out                  # arquivos estáticos gerados com `npx next export`
 ┣ 📄 README.md
 ┣ 📄 template.yaml        # (opcional) CloudFormation para infra S3 + CloudFront
```

---

## 🧹 Como limpar os recursos

- Excluir arquivos do bucket
- Deletar bucket S3
- Remover distribuição CloudFront
- Excluir zona hospedada do Route 53
- Cancelar domínio na Freenom (opcional)

---

## 🧠 Decisões de Design

- Utilizar site estático por simplicidade e custo zero
- CloudFront para acelerar entrega global e melhorar performance
- Route 53 pela integração simples com domínio e AWS
- Freenom para domínio gratuito viável

---

## 📊 Diagrama de Arquitetura

```
Navegador ─► DNS Route 53 ─► CloudFront ─► Bucket S3 (Website Hosting)
                        ▲
                        │
                 Domínio Freenom
```

---

## 💰 Estimativa de Custos

| Serviço      | Plano                     | Custo Estimado |
|--------------|----------------------------|----------------|
| AWS S3       | Camada gratuita (5 GB)     | R$ 0           |
| CloudFront   | Camada gratuita (1 TB/mês) | R$ 0           |
| Route 53     | 1 zona + 1 domínio         | R$ 0 (somente se domínio Freenom) |
| Freenom      | Domínio `.tk` gratuito     | R$ 0           |

Total estimado: **R$ 0,00**

---

## 🎥 Vídeo Pitch

👉 Link para vídeo explicando a arquitetura, decisões e custo (adicionar link):  
[YouTube Pitch - Blog Estático AWS](https://link-do-video)

---

## 🧾 Repositório com Código-Fonte e IaC

📁 GitHub com código e template CloudFormation:  
[https://github.com/usuario/projeto-blog-s3-cloudfront](https://github.com/usuario/projeto-blog-s3-cloudfront)

---

## 👨‍💻 Autoria

Desenvolvido por alunos da FATEC Itapira – 6º Semestre – Computação em Nuvem 2
