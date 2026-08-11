# Melhorias no site Tech Noda + estrutura de mockups para leads

Data: 2026-08-11

## Contexto

Landing page única (`technoda-landing.html`) para a Tech Noda, empresa de criação de sites,
atendimento remoto para todo o Brasil. Site já tem domínio próprio (technodaoficial.com) com
hospedagem ativa (Vercel/Netlify/GitHub Pages). Este diretório local ainda não era um repositório
git.

## Objetivo

1. Reforçar a fundação de SEO da página (hoje só existe `<title>`, sem meta description, Open
   Graph, canonical, favicon ou schema markup).
2. Ajustar pontos de copy com linguagem hesitante, seguindo boas práticas de conversão de 2026
   (CTA orientado a benefício, headline clara, remoção de hedging).
3. Corrigir o número de WhatsApp (placeholder → `5543991772110`).
4. Criar uma estrutura de pastas para que cada mockup enviado a um lead tenha sua própria URL em
   `technodaoficial.com/mockup-lead/<slug-do-lead>`, sem que essas páginas sejam indexadas pelo
   Google (são material de vendas, não conteúdo público).

## Fora de escopo

- Redesign visual — o sistema de design atual (tema "blueprint") já é coeso e moderno.
- Depoimentos/cases reais — não inventamos conteúdo; se o usuário fornecer, entra depois.
- Deploy de fato no provedor de hospedagem — não temos credenciais da conta; entregamos os
  arquivos organizados para o fluxo de deploy que o usuário já usa.

## Design

### 1. `index.html` (renomeado de `technoda-landing.html`)

Hosts estáticos (Vercel/Netlify/GitHub Pages) servem `index.html` na raiz por padrão — o arquivo é
renomeado para isso funcionar sem configuração extra.

Adições no `<head>`:
- `<meta name="description">` (150–160 caracteres, benefício direto)
- Open Graph (`og:title`, `og:description`, `og:type`, `og:url`, `og:locale`) e Twitter Card
- `<link rel="canonical" href="https://technodaoficial.com/">`
- `<link rel="icon">` (favicon simples, reaproveitando a cor coral/cyan da marca)
- JSON-LD `ProfessionalService` (sem endereço fixo — atendimento remoto nacional)

Ajustes de copy (mantendo tom e estrutura atuais):
- Seção "O problema": remover hedging ("pode acabar procurando") por afirmações mais diretas.
- Microcopy de CTAs secundários revisada para reforçar benefício.

Correção técnica:
- `WHATSAPP_NUMBER` no script final: `5544900000000` → `5543991772110`.

### 2. `robots.txt` e `sitemap.xml` na raiz

- `robots.txt` permite indexação geral do site e bloqueia explicitamente `/mockup-lead/`.
- `sitemap.xml` lista apenas a home (`/`) — páginas de mockup-lead não entram no sitemap.

### 3. `mockup-lead/` — estrutura para mockups de leads

```
mockup-lead/
  _template/index.html   ← ponto de partida para cada novo mockup
```

- `_template/index.html`: versão mínima de partida (não é o site da Tech Noda, é um esqueleto
  para adaptar ao negócio do lead), com `<meta name="robots" content="noindex,nofollow">` já
  incluído.
- Fluxo de uso: copiar `_template/` para `mockup-lead/<slug-do-lead>/`, editar o conteúdo para o
  negócio do lead, publicar. URL resultante: `technodaoficial.com/mockup-lead/<slug-do-lead>`.
- Cada pasta de lead criada futuramente deve manter a tag `noindex,nofollow` — é o que impede que
  esses mockups concorram com o site oficial nos resultados de busca.

## Teste / verificação

- Abrir `index.html` localmente no navegador e revisar visualmente (nenhuma mudança estrutural de
  layout/CSS, só `<head>` e pequenos trechos de texto).
- Validar JSON-LD com o Rich Results Test (colar o HTML ou a URL depois do deploy).
- Confirmar que o link do WhatsApp abre a conversa certa (`wa.me/5543991772110`).
- Confirmar que `mockup-lead/_template/index.html` tem `noindex,nofollow` no `<head>`.
