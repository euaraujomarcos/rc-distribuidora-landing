# Landing Page — RC Distribuidora de Pisos e Porcelanatos

Landing page de captura de leads em arquivo único (`index.html`), sem dependências de build. Basta abrir no navegador para visualizar e hospedar em qualquer serviço de site estático.

## Estratégia de conversão

- **Todos os CTAs levam ao WhatsApp** (34) 99887-1579 com mensagem pré-preenchida.
- **Formulário do hero** monta a mensagem com nome, telefone, interesse e detalhes, e abre o WhatsApp — o lead chega qualificado.
- **Cards de produto** enviam mensagem específica ("gostaria de saber os preços de Porcelanato"), útil para identificar a origem do interesse.
- **Botão flutuante** de WhatsApp em todas as resoluções.
- Função `trackLead()` dispara `Lead` (Meta Pixel) e `generate_lead` (GA4/Google Ads) em todo clique de conversão.

## Antes de publicar — checklist

1. **Pixels**: colar os snippets do Meta Pixel e do Google Tag nos comentários indicados no `<head>` do `index.html`.
2. **Depoimentos**: já preenchidos com 3 avaliações reais do Google (Emanuel de Paula, José Junior e Isaías de Souza Marinho Júnior — todas 5 estrelas). O depoimento do Emanuel foi levemente resumido com "(…)".
3. **Números da barra de confiança** ("+20 anos", "Milhares de obras"): confirmar com o cliente e ajustar.
4. **Fotos dos cards**: usam imagens de ambientes dos catálogos oficiais dos fabricantes parceiros, salvas em `assets/` (já otimizadas para web). Como a RC é revendedora autorizada, o uso é praxe do mercado — mas vale confirmar com os representantes das marcas. Origem: `villagres-*.webp` (Villagres), `helena-*.jpg` (Helena Porcelanato), `majopar-*.jpg` (Majopar).
5. **Logos das marcas**: substituir os chips de texto pelos logos oficiais, se autorizado pelos fabricantes.
6. **Número do WhatsApp**: configurado em `WHATSAPP_NUMBER` no `<script>` ao final do arquivo.

## Otimizações de conversão (metodologia Oli Gardner / Unbounce)

- **Attention Ratio**: links de fuga removidos (Instagram saiu do rodapé e do bloco de contato). Mantidos por decisão consciente: link de avaliações no Google (credibilidade) e telefone/e-mail (canais de contato que também geram lead).
- **Message match por URL** — a headline troca conforme o parâmetro `?h=` para casar com o texto de cada anúncio:
  - `?h=porcelanato` · `?h=amadeirado` · `?h=ceramico` · `?h=obra` · `?h=reforma`
  - `?produto=Porcelanato` pré-seleciona o campo "O que você procura?" do formulário (aceita o texto exato de qualquer opção do select).
  - As duas podem ser combinadas: `/?h=amadeirado&produto=Porcelanato`
  - Para criar novas variações, edite o objeto `HEADLINES` no `<script>`.
- **Urgência**: badge "Resposta rápida em horário comercial" no formulário. Há também uma barra de promoção opcional — configure `PROMO_TEXT` no `<script>` com uma oferta REAL confirmada com a loja (deixe vazio para ocultar).
- **Mobile conversion-centered** (breakpoint 600px):
  - Barra fixa de WhatsApp no rodapé da tela (substitui o botão flutuante redondo) — CTA sempre visível com alvo de toque de tela inteira.
  - Um CTA dominante por tela: o botão "Preencher formulário" some no hero (o formulário está logo abaixo) e os CTAs viram largura total com min-height 54px.
  - Depoimentos em carrossel horizontal com scroll-snap — prova social completa com menos rolagem vertical.
  - Inputs com fonte 16px (evita zoom automático do iOS) e âncoras com `scroll-margin-top` para não sumirem sob o header fixo.

## Hospedagem sugerida

Qualquer host estático funciona: Netlify, Vercel, Cloudflare Pages ou o próprio provedor atual do domínio. Para campanhas, publicar em um caminho tipo `rcdistribuidoradepisos.com.br/orcamento` ou subdomínio `promo.rcdistribuidoradepisos.com.br`.

## Design system v2 — "Editorial de arquitetura" (29/07/2026)

Redesign após feedback do cliente (referência dele: https://carolvilarinhodev.github.io/teste/). O design system se inspira em catálogos de porcelanato de alto padrão e sites de estúdios de arquitetura:

- **Tipografia**: Fraunces (serifada expressiva, títulos — com itálicos de destaque) + Manrope (UI/corpo).
- **Neutros de galeria**: fundo plaster `#F4F2EC`, hairlines `#E3DED2` — as cores da marca entram como acento, não como fundo de tudo.
- **Dispositivos editoriais**: seções numeradas (01–07), hairlines separando conteúdos, micro-labels em caixa alta com tracking largo, números serifados nas estatísticas, legendas nas fotos.
- **Mantido da versão do cliente**: painéis arredondados sobre fundo colorido, a casinha SVG que se constrói com o scroll (recolorida para tom blueprint/stone), estrutura de seções, dados atualizados (endereço, marcas em 3 categorias, 15+ marcas).
- **Mantido da nossa v1** (que a versão do cliente havia perdido): message match `?h=`/`?produto=`, `PROMO_TEXT`, `trackLead()` ativo, máscara de telefone, validação do formulário, mensagens de WhatsApp específicas por produto (`data-produto`), barra fixa mobile.
- **Mobile first**: headline visível antes da foto no hero, carrosséis scroll-snap (produtos e depoimentos), CTAs full-width ≥54px, barra fixa de WhatsApp com `safe-area-inset`.

## Identidade visual

Cores extraídas pixel a pixel da logo oficial (`Arquivos/Logo RC Distribuídora Matriz.jpg`), definidas como variáveis CSS no topo do `index.html`:

| Cor | Hex | RGB | Uso na página |
| --- | --- | --- | --- |
| Azul-marinho | `#03134F` | rgb(3, 19, 79) | Seções escuras (barra de confiança, CTA final, rodapé), badge do logo |
| Azul royal | `#043282` | rgb(4, 50, 130) | Acentos, títulos em destaque, links, ícones |
| Amarelo RC | `#FCBC02` | rgb(252, 188, 2) | Botão principal do formulário, números de destaque, estrelas |

Os botões de WhatsApp permanecem verdes (`#1fa855`) de propósito — verde é a cor universalmente associada ao WhatsApp e converte melhor que botão na cor da marca.

## Dados da empresa (extraídos do site atual em 21/07/2026)

- Rua João Thomaz de Rezende, 560 — Osvaldo Rezende, Uberlândia/MG (endereço confirmado pelo cliente em 29/07/2026; o site antigo listava outro)
- Tel: (34) 3211-9950 · WhatsApp: (34) 99887-1579
- contato@rcdistribuidoradepisos.com.br · @rcdistribuidoramatriz

## Marcas parceiras (atualizadas pelo cliente em 29/07/2026)

- **Pisos e porcelanatos**: Majopar · Villagres · Helena · Delta · Incefra · InOut · Duragres · Viva · Ceral · Strufaldi · Atlas · Morandin
- **Louças**: Celite · Roca
- **Metais**: Gold Flex · Celite · Incepa · Fani
