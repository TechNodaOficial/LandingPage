# Animações e efeitos visuais — LP e páginas de exemplo

Data: 2026-08-12

## Contexto

Três páginas estáticas (HTML/CSS/JS puro, sem build): `index.html` (LP da Tech Noda), `exemplo-petshop/index.html`, `exemplo-advogado/index.html`. Cada uma já tem uma identidade visual própria e consolidada. O pedido é adicionar animações/efeitos, com liberdade criativa do usuário para o assistente escolher, sem migrar para React (decisão já tomada: overhead de build/deploy não se justifica para o ganho, quando CSS/JS puro já cobre o que é pedido).

## Objetivo

Adicionar movimento e polimento a cada página, coerente com a identidade visual já existente de cada uma, sem introduzir dependências externas (sem GSAP, sem frameworks) e respeitando `prefers-reduced-motion` em todos os efeitos novos.

## Fora de escopo

- Migração para React ou qualquer framework.
- Bibliotecas de animação externas.
- Mudança de conteúdo, copy ou estrutura de seções — só movimento/efeitos visuais sobre o que já existe.

## Design por página

### `index.html` (identidade "prancheta técnica")

1. **Reveal em cascata**: o `IntersectionObserver` existente (`.reveal` → `.in`) passa a aplicar um `transition-delay` incremental aos filhos diretos de `.grid-3`, `.grid-4`, `.feature-grid`, `.who-grid` e `.grid-benefits` quando o pai entra em vista, em vez de todos os itens aparecerem no mesmo instante.
2. **Momento de assinatura no hero**: os 4 cantos do `.device-plate` desenham a partir do vértice (stroke-draw via `clip-path` ou `transform: scale` a partir da origem) ao carregar; uma faixa de "scan" (gradiente claro) atravessa a `.screen` do mockup uma vez, em loop lento e sutil.
3. **Linha de processo**: a régua pontilhada de `.process-list::before` (seção 4) e a linha do `.timeline` (seção 9) passam a se desenhar progressivamente conforme a seção entra em vista (`stroke-dashoffset` animado via um `<svg>` sobre a linha, ou `clip-path: inset()` animado no `::before` existente). Os `.step .node` e `.tl-node .dot` recebem um pulso de escala (1 → 1.15 → 1) no momento em que entram em vista.
4. **Botões**: `.btn-primary` e `.nav-cta` recebem `:active{transform:scale(0.96)}` para feedback tátil ao clique, além do hover já existente.

### `exemplo-petshop/index.html` (identidade divertida/arredondada)

1. Patinhas de fundo (`.paw-bg` do hero) recebem duas camadas com `background-position` animando em loop lento e em direções levemente diferentes (efeito parallax simples, sem JS de scroll).
2. `.vcard` (cards de serviço) entram com um pequeno "bounce" (`cubic-bezier` com overshoot) escalonado, reaproveitando o mesmo `IntersectionObserver` que a LP usa, adaptado a este arquivo.
3. A ilustração do cão/gato (`.pet-illustration`) recebe uma animação de loop simples e sutil (ex: o rabo do gato — path já existe em `stroke` — balança poucos graus via CSS `@keyframes` em `transform-origin`).

### `exemplo-advogado/index.html` (identidade editorial/séria)

1. Reveal ao rolar: fade + leve subida (8–12px), sem bounce, aplicado às seções principais (hero, strip, articles, bulletin, contact) via o mesmo padrão de `IntersectionObserver`.
2. Números do `.hero-card .stat` (68%, 9 anos) sobem contando de 0 até o valor final quando o card entra em vista, via um pequeno helper JS de contagem (parseia o texto atual, anima com `requestAnimationFrame`).
3. Links de navegação e "Ver todos os artigos →" recebem sublinhado que se desenha da esquerda para a direita no hover (`background-image` linear ou `::after` com `transform: scaleX`).

## Acessibilidade

Todo efeito novo (nas 3 páginas) é envolvido por `@media (prefers-reduced-motion: reduce)` que desativa a animação e mostra o estado final diretamente — mesmo padrão que `index.html` já usa para o `.reveal` existente.

## Verificação

Sem test runner (páginas estáticas). Verificação por inspeção visual: renderizar cada página via Chrome headless (screenshot) antes/depois, e checagem manual de que:
- Nenhum layout existente foi alterado (só propriedades de animação/transição adicionadas).
- Os três arquivos abrem sem erros de console.
- Com `prefers-reduced-motion: reduce` simulado, os elementos aparecem no estado final sem animação.
