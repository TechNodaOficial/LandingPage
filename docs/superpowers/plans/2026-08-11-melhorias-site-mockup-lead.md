# Melhorias SEO/copy no site Tech Noda + estrutura mockup-lead Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Adicionar fundação de SEO e ajustes de copy em `index.html`, corrigir o número de WhatsApp, e criar a estrutura `mockup-lead/` para publicar mockups de leads sem que sejam indexados pelo Google.

**Architecture:** Site estático de arquivo único (`index.html`) hospedado via Vercel/Netlify/GitHub Pages a partir do repositório `TechNodaOficial/LandingPage`. Não há framework, build step ou test runner — "testar" aqui significa verificar o conteúdo exato do HTML gerado (via `grep`/inspeção) e, quando possível, abrir no navegador. Nenhuma mudança estrutural de CSS/layout.

**Tech Stack:** HTML5, CSS puro, JavaScript vanilla (inline), sem dependências de build.

## Global Constraints

- Domínio de produção: `https://technodaoficial.com/` (usar essa URL exata em canonical/OG/schema).
- Número de WhatsApp correto: `5543991772110` (código do país 55 + DDD 43 + número, só dígitos).
- Idioma do site: `pt-BR` — todo texto novo em português do Brasil.
- Não alterar CSS/layout existente — só `<head>`, dois trechos de copy, e arquivos novos.
- Páginas em `mockup-lead/` NUNCA devem ser indexadas pelo Google — toda página nova nessa pasta precisa de `<meta name="robots" content="noindex,nofollow">`.
- Não inventar depoimentos, cases ou métricas fictícias.

---

### Task 1: SEO fundamentals no `<head>` do `index.html`

**Files:**
- Modify: `index.html:1-9` (dentro de `<head>`, depois do `<title>` existente na linha 6)

**Interfaces:**
- Produces: tags `<meta name="description">`, Open Graph, Twitter Card, `<link rel="canonical">`, `<link rel="icon">`, `<script type="application/ld+json">` no `<head>` — nenhum outro task depende dessas tags.

- [ ] **Step 1: Adicionar as meta tags de SEO e o schema JSON-LD**

Abrir `index.html` e, imediatamente depois da linha 6 (`<title>Tech Noda — Sua empresa online, do jeito certo</title>`) e antes da linha 7 (`<link rel="preconnect" href="https://fonts.googleapis.com">`), inserir:

```html
<meta name="description" content="Criamos sites profissionais, rápidos e personalizados para sua empresa. Atendimento remoto para todo o Brasil. Peça seu orçamento pelo WhatsApp.">
<link rel="canonical" href="https://technodaoficial.com/">
<link rel="icon" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 32 32'%3E%3Crect width='32' height='32' fill='%230E2F45'/%3E%3Ccircle cx='16' cy='16' r='6' fill='%23FF6A4D'/%3E%3C/svg%3E">

<meta property="og:type" content="website">
<meta property="og:title" content="Tech Noda — Sua empresa online, do jeito certo">
<meta property="og:description" content="Criamos sites profissionais, rápidos e personalizados para sua empresa. Atendimento remoto para todo o Brasil.">
<meta property="og:url" content="https://technodaoficial.com/">
<meta property="og:locale" content="pt_BR">
<meta name="twitter:card" content="summary">
<meta name="twitter:title" content="Tech Noda — Sua empresa online, do jeito certo">
<meta name="twitter:description" content="Criamos sites profissionais, rápidos e personalizados para sua empresa. Atendimento remoto para todo o Brasil.">

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "ProfessionalService",
  "name": "Tech Noda",
  "description": "Criação de sites profissionais, rápidos e personalizados para empresas, com atendimento remoto para todo o Brasil.",
  "url": "https://technodaoficial.com/",
  "telephone": "+5543991772110",
  "areaServed": "BR"
}
</script>
```

- [ ] **Step 2: Verificar que as tags foram inseridas corretamente**

Run: `grep -c "og:title\|application/ld+json\|rel=\"canonical\"\|name=\"description\"" "C:\Users\User\Desktop\Eu\Tech Noda\LP\index.html"`
Expected: retorna um número ≥ 4 (uma ocorrência por tag buscada, sem erro de sintaxe HTML — abrir o arquivo num navegador local deve continuar mostrando a página normalmente, sem mudança visual).

- [ ] **Step 3: Commit**

```bash
cd "C:\Users\User\Desktop\Eu\Tech Noda\LP"
git add index.html
git commit -m "Add SEO meta tags, favicon and JSON-LD schema to index.html"
```

---

### Task 2: Corrigir número de WhatsApp e firmar copy hesitante

**Files:**
- Modify: `index.html:464` (parágrafo da seção "O problema")
- Modify: `index.html:799` (constante `WHATSAPP_NUMBER` no script)

**Interfaces:**
- Consumes: nenhuma (edição de texto isolada).
- Produces: nenhuma (não há outro task que dependa deste texto).

- [ ] **Step 1: Substituir a frase com hedging na seção "O problema"**

Encontrar em `index.html` (linha 464):

```html
        <p>Quando alguém encontra sua empresa no Google, Instagram ou indicação, uma das primeiras coisas que pode fazer é procurar mais informações. Se não encontra um site profissional, pode acabar procurando outra empresa que transmita mais confiança.</p>
```

Substituir por:

```html
        <p>Quando alguém encontra sua empresa no Google, Instagram ou indicação, a primeira coisa que faz é procurar mais informações. Sem um site profissional, esse cliente vai para a concorrência que transmite mais confiança.</p>
```

- [ ] **Step 2: Corrigir o número de WhatsApp**

Encontrar em `index.html` (linha 799):

```javascript
  const WHATSAPP_NUMBER = "5544900000000"; // <-- troque pelo número real da Tech Noda
```

Substituir por:

```javascript
  const WHATSAPP_NUMBER = "5543991772110";
```

- [ ] **Step 3: Verificar as duas substituições**

Run: `grep -n "5544900000000\|pode acabar procurando" "C:\Users\User\Desktop\Eu\Tech Noda\LP\index.html"`
Expected: nenhuma linha retornada (texto antigo e número antigo não existem mais).

Run: `grep -n "5543991772110\|esse cliente vai para a concorrência" "C:\Users\User\Desktop\Eu\Tech Noda\LP\index.html"`
Expected: duas linhas retornadas (uma por trecho novo).

- [ ] **Step 4: Commit**

```bash
cd "C:\Users\User\Desktop\Eu\Tech Noda\LP"
git add index.html
git commit -m "Fix WhatsApp number and firm up hedging copy in problem section"
```

---

### Task 3: `robots.txt` e `sitemap.xml`

**Files:**
- Create: `robots.txt`
- Create: `sitemap.xml`

**Interfaces:**
- Produces: regra `Disallow: /mockup-lead/` em `robots.txt` — Task 4 depende desta regra existir para que as páginas de mockup-lead fiquem duplamente protegidas (regra no robots.txt + meta tag noindex por página).

- [ ] **Step 1: Criar `robots.txt`**

```
User-agent: *
Allow: /
Disallow: /mockup-lead/

Sitemap: https://technodaoficial.com/sitemap.xml
```

- [ ] **Step 2: Criar `sitemap.xml`**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://technodaoficial.com/</loc>
  </url>
</urlset>
```

- [ ] **Step 3: Verificar os dois arquivos**

Run: `grep -c "Disallow: /mockup-lead/" "C:\Users\User\Desktop\Eu\Tech Noda\LP\robots.txt"`
Expected: `1`

Run: `grep -c "https://technodaoficial.com/" "C:\Users\User\Desktop\Eu\Tech Noda\LP\sitemap.xml"`
Expected: `1`

- [ ] **Step 4: Commit**

```bash
cd "C:\Users\User\Desktop\Eu\Tech Noda\LP"
git add robots.txt sitemap.xml
git commit -m "Add robots.txt and sitemap.xml, blocking mockup-lead from indexing"
```

---

### Task 4: Template `mockup-lead/_template/index.html`

**Files:**
- Create: `mockup-lead/_template/index.html`
- Create: `mockup-lead/README.md`

**Interfaces:**
- Consumes: regra `Disallow: /mockup-lead/` de `robots.txt` (Task 3) — a tag `noindex,nofollow` desta página é a segunda camada de proteção, independente da primeira.
- Produces: nenhuma (é o ponto final da cadeia — futuras pastas de lead copiam este arquivo).

- [ ] **Step 1: Criar o template mínimo do mockup**

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="robots" content="noindex,nofollow">
<title>[NOME DA EMPRESA DO LEAD] — Mockup</title>
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Sans+Condensed:wght@600;700&family=IBM+Plex+Sans:wght@400;500;600&display=swap" rel="stylesheet">
<style>
  :root{ --ink:#0E2F45; --paper:#F5F2EA; --coral:#FF6A4D; --text-dark:#16232B; --text-mute:#5A6B70; }
  *{box-sizing:border-box; margin:0; padding:0;}
  body{background:var(--paper); color:var(--text-dark); font-family:'IBM Plex Sans',sans-serif; line-height:1.5;}
  .wrap{max-width:960px; margin:0 auto; padding:0 24px;}
  h1,h2{font-family:'IBM Plex Sans Condensed',sans-serif; font-weight:700;}
  header{background:var(--ink); color:#EEF3F2; padding:90px 0 60px;}
  header h1{font-size:clamp(28px,4vw,46px); max-width:640px;}
  header p{margin-top:16px; font-size:16px; color:rgba(238,243,242,0.75); max-width:480px;}
  section{padding:64px 0;}
  section h2{font-size:26px; margin-bottom:28px;}
  .services{display:grid; grid-template-columns:repeat(3,1fr); gap:20px;}
  .services div{background:#fff; border:1px solid #DAD4C4; padding:22px;}
  .services h3{font-size:16px; margin-bottom:8px;}
  .services p{font-size:14px; color:var(--text-mute);}
  .contact{background:var(--ink); color:#EEF3F2; text-align:center; padding:70px 0;}
  .contact a{display:inline-block; margin-top:20px; background:var(--coral); color:#fff; padding:14px 28px; font-weight:600; text-decoration:none;}
  @media(max-width:760px){ .services{grid-template-columns:1fr;} }
</style>
</head>
<body>

<header>
  <div class="wrap">
    <h1>[Frase de destaque do negócio do lead]</h1>
    <p>[Uma frase curta explicando o que a empresa do lead faz e para quem.]</p>
  </div>
</header>

<section>
  <div class="wrap">
    <h2>Serviços</h2>
    <div class="services">
      <div><h3>[Serviço 1]</h3><p>[Descrição curta]</p></div>
      <div><h3>[Serviço 2]</h3><p>[Descrição curta]</p></div>
      <div><h3>[Serviço 3]</h3><p>[Descrição curta]</p></div>
    </div>
  </div>
</section>

<section class="contact">
  <div class="wrap">
    <h2>Fale com a gente</h2>
    <a href="https://wa.me/5543991772110" target="_blank" rel="noopener">Falar no WhatsApp</a>
  </div>
</section>

</body>
</html>
```

- [ ] **Step 2: Criar o README explicando o fluxo de uso**

```markdown
# mockup-lead/

Cada mockup enviado para um lead vira uma pasta aqui dentro, com sua própria URL:
`technodaoficial.com/mockup-lead/<slug-do-lead>`

## Como criar um novo mockup

1. Copie a pasta `_template/` para `mockup-lead/<slug-do-lead>/` (ex: `mockup-lead/pizzaria-do-joao/`).
2. Edite `index.html` dentro da nova pasta: troque tudo entre `[colchetes]` pelo conteúdo real do lead.
3. **Não remova** a linha `<meta name="robots" content="noindex,nofollow">` — ela impede que o Google indexe o mockup como se fosse um site de cliente de verdade.
4. Publique (deploy normal do repositório). A URL final é `technodaoficial.com/mockup-lead/<slug-do-lead>`.

Essas páginas são material de vendas, não conteúdo do site oficial — por isso ficam bloqueadas em `robots.txt` e marcadas como `noindex`.
```

- [ ] **Step 3: Verificar a proteção contra indexação**

Run: `grep -c "noindex,nofollow" "C:\Users\User\Desktop\Eu\Tech Noda\LP\mockup-lead\_template\index.html"`
Expected: `1`

- [ ] **Step 4: Commit**

```bash
cd "C:\Users\User\Desktop\Eu\Tech Noda\LP"
git add mockup-lead
git commit -m "Add mockup-lead template and usage instructions"
```
