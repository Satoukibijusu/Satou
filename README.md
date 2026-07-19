# Satou (Portfolio) (Web3 Content Creator)

Site institucional estático: HTML5, CSS3 e JavaScript puro, sem frameworks e sem build tools. Pronto para deploy direto no GitHub Pages ou Netlify (basta apontar para a raiz do projeto).

## Estrutura

```
portfolio/
├── index.html
├── case-studies/
│   ├── case-template.html   → template genérico e comentado para novos cases (sem dados reais)
│   ├── pagfinance.html      → case real (versão completa: timeline semanal, 3 destaques, 5 KPIs, insights + lições)
│   ├── amulets.html         → case real (versão enxuta: sem timeline, 1 destaque, 3 KPIs, 1 insight em texto)
│   └── merge.html           → case real (mesma versão enxuta da Amulets)
├── assets/
│   ├── logos/         → logos de empresas/parceiros (marquee "Brands I've Worked With" + cards de Case Study)
│   ├── images/         → imagens gerais de campanhas/seções
│   ├── screenshots/    → screenshots/preview dos cards de Case Study e Content
│   ├── characters/     → ilustrações do personagem (uma por "pose"/seção)
│   ├── nodra/           → ilustrações da seção Nodra
│   └── testimonials/    → fotos placeholder de depoimentos
├── css/
│   ├── style.css        → tokens de design, base, tipografia e TODOS os componentes compartilhados
│   │                       (nav, footer, botões, cards, dashboard, reason-cards etc.)
│   ├── case-study.css    → estilos EXCLUSIVOS das páginas de Case Study (hero da página, breadcrumb,
│   │                       timeline de execução, highlight cards, CTA final). Nunca duplica nada que já
│   │                       exista em style.css, apenas consome as mesmas variáveis/tokens.
│   ├── animations.css    → keyframes e utilitários de scroll-reveal
│   └── responsive.css    → breakpoints (1024 / 860 / 768 / 480px)
├── js/
│   └── main.js           → módulos: nav, idioma, scroll-reveal, contadores (usado por todas as páginas,
│                            incluindo as de case-studies/, sem nenhuma alteração necessária)
└── README.md
```

## Status do desenvolvimento

Todas as etapas estruturais da landing estão concluídas (Hero, Brands, Production, Real Data, Proof of Results, Nodra, Differentiators, Testimonials, Contact, Footer), incluindo o sistema de páginas de Case Study dedicadas.

## Como rodar localmente

Não há dependências nem build. Basta abrir `index.html` diretamente no navegador, ou servir a pasta com qualquer servidor estático (recomendado para evitar bloqueios de CORS em alguns navegadores):

```bash
npx serve .
# ou
python3 -m http.server 8080
```

## Idiomas (PT / EN)

Todo texto traduzível usa dois elementos irmãos com `data-lang="pt"` e `data-lang="en"`. O JS alterna uma classe no `<body>` (`lang-pt` / `lang-en`) que mostra/esconde cada um via CSS. Português é o idioma padrão.

Para adicionar um novo texto bilíngue:
```html
<span data-lang="pt">Texto em português</span>
<span data-lang="en">Text in English</span>
```

## Case Studies: como adicionar um novo

1. Duplique `case-studies/case-template.html` como `case-studies/<slug>.html`.
2. Preencha os placeholders entre colchetes com dados reais (nunca invente números ou citações).
3. Use a versão completa (timeline, 3 destaques, 5 KPIs) só quando houver dado semanal granular; caso
   contrário, siga o padrão enxuto de `amulets.html`/`merge.html` (sem timeline, 1 destaque, `.kpis-3`,
   insight único em texto). O próprio `case-template.html` documenta as duas opções em comentários.
4. Adicione um novo `<a class="case-card">` na grade de Case Studies em `index.html`, apontando para a
   página nova.
5. Não crie CSS novo: todo componente reaproveitável já existe em `style.css` (compartilhado) ou
   `case-study.css` (exclusivo de Case Study). Se sentir falta de um padrão visual novo, procure nesses
   dois arquivos primeiro.

## Substituindo assets (placeholders)

- **Personagem**: `assets/characters/character-hero.svg` é o placeholder da pose do Hero. Basta substituir o arquivo (mesmo nome ou atualizando o `src` no HTML); a proporção do container (`.hero-visual-frame`, aspect-ratio 13:16) já está definida, então a arte final só precisa respeitar esse enquadramento.
- **Logos** (`assets/logos/`): logos reais de marcas com parceria oficial concluída (esteira "Brands I've Worked With") e dos 3 Case Studies ativos (PagFinance, Amulets, Merge). Basta substituir o arquivo pelo logo real, mantendo o mesmo nome; a altura do container já é fixa (52px na esteira, 20px no card de case study, 32px no hero da página de case study), então qualquer SVG/PNG bem enquadrado horizontalmente encaixa sem ajuste de CSS.
- **Screenshots dos Case Studies** (`assets/screenshots/`): `case-placeholder-a.svg` (PagFinance), `case-amulets.svg`, `case-merge.svg`. São placeholders com proporção 400×460; substituir por prints reais dos posts respeitando essa proporção (ou próxima) mantém o layout do card intacto. Os arquivos `case-rapidz.svg`, `case-mmerge.svg`, `case-chainless.svg` e os logos `blockchainrio.png`/`mmerge.png` ficaram órfãos após a limpeza dos cases antigos; foram mantidos no projeto (não removidos) caso sirvam para um futuro case study, mas não estão referenciados em nenhuma página no momento.
- **Depoimentos**: estrutura pronta em `#testimonials`, aguardando conteúdo real; troca de arquivo/texto sem alteração de layout.
- **Links dos Case Studies**: o Instagram e o LinkedIn (Contact e Footer) têm `<!-- TODO -->` marcando URLs ainda não confirmadas.

## Convenções de código

- CSS organizado por seções numeradas dentro de cada arquivo (ver comentários `/* ---- N. NOME ---- */`).
- Classes seguem padrão `bloco-elemento` simples (sem metodologia BEM completa, mas consistente: ex. `.hero`, `.hero-title`, `.hero-stat`, `.hero-stat-value`), com modificadores via `--` (ex. `.dash-card--age`) e estados via `is-` (ex. `.is-visible`, `.is-scrolled`).
- JS organizado em módulos IIFE independentes (`LangToggle`, `Nav`, `ScrollReveal`, `Counters`), cada um com seu próprio `init()`, inicializados uma vez em `DOMContentLoaded`. Novas seções e novas páginas devem reaproveitar esse mesmo `js/main.js` sem modificá-lo.
- Animações respeitam `prefers-reduced-motion`.
- Duplicação entre páginas: como o projeto é HTML puro sem build step, o nav e o footer são duplicados (verbatim) em cada arquivo `.html`. É uma limitação inerente a essa arquitetura (sem framework, sem includes), não descuido; ao alterar nav ou footer, replique a mudança em todos os arquivos `.html` do projeto.
