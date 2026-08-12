# mockup-lead/

Cada mockup enviado para um lead vira uma pasta aqui dentro, com sua própria URL:
`technodaoficial.com/mockup-lead/<slug-do-lead>`

## Como criar um novo mockup

1. Copie a pasta `_template/` para `mockup-lead/<slug-do-lead>/` (ex: `mockup-lead/pizzaria-do-joao/`).
2. Edite `index.html` dentro da nova pasta: troque tudo entre `[colchetes]` pelo conteúdo real do lead.
3. Troque também o placeholder `[NUMERO-WHATSAPP-DO-LEAD]` no link do WhatsApp pelo número real do lead, apenas dígitos, com código do país e DDD (ex: `5543991772110`).
4. **Não remova** a linha `<meta name="robots" content="noindex,nofollow">` — ela impede que o Google indexe o mockup como se fosse um site de cliente de verdade.
5. Publique (deploy normal do repositório). A URL final é `technodaoficial.com/mockup-lead/<slug-do-lead>`.

Essas páginas são material de vendas, não conteúdo do site oficial — por isso ficam marcadas como `noindex`.

**Nunca** adicione páginas de `mockup-lead/` ao `sitemap.xml`. Elas não são conteúdo indexável do site, são material de vendas para leads específicos.

Se um mockup for aprovado e se tornar o site real e definitivo do lead, remova a linha `<meta name="robots" content="noindex,nofollow">` dessa página antes de publicá-la de verdade — caso contrário, o site real do cliente nunca seria indexado pelo Google.
