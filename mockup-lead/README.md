# mockup-lead/

Cada mockup enviado para um lead vira uma pasta aqui dentro, com sua própria URL:
`technodaoficial.com/mockup-lead/<slug-do-lead>`

## Como criar um novo mockup

1. Copie a pasta `_template/` para `mockup-lead/<slug-do-lead>/` (ex: `mockup-lead/pizzaria-do-joao/`).
2. Edite `index.html` dentro da nova pasta: troque tudo entre `[colchetes]` pelo conteúdo real do lead.
3. **Não remova** a linha `<meta name="robots" content="noindex,nofollow">` — ela impede que o Google indexe o mockup como se fosse um site de cliente de verdade.
4. Publique (deploy normal do repositório). A URL final é `technodaoficial.com/mockup-lead/<slug-do-lead>`.

Essas páginas são material de vendas, não conteúdo do site oficial — por isso ficam bloqueadas em `robots.txt` e marcadas como `noindex`.