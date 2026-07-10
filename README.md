# Satou — Portfolio (Web3 Content Creator)

Site institucional estático — HTML5, CSS3 e JavaScript puro, sem frameworks e sem build tools. Pronto para deploy direto no GitHub Pages ou Netlify (basta apontar para a raiz do projeto).

## Estrutura

```
portfolio/
├── index.html
├── assets/
│   ├── logos/         → logos de empresas/parceiros (marquee de "Companies")
│   ├── images/         → imagens gerais de campanhas/seções
│   ├── screenshots/    → screenshots reais de posts/threads/vídeos
│   ├── characters/     → ilustrações do personagem (uma por "pose"/seção)
│   └── icons/          → ícones SVG utilitários
├── css/
│   ├── style.css        → tokens de design, base, tipografia, componentes
│   ├── animations.css    → keyframes e utilitários de scroll-reveal
│   └── responsive.css    → breakpoints (1024 / 860 / 768 / 480px)
├── js/
│   └── main.js           → módulos: nav, idioma, scroll-reveal, contadores
└── README.md
```

## Status do desenvolvimento

- [x] **Etapa 1** — Estrutura do projeto, Navegação, Hero
- [ ] Etapa 2 — Companies, At a Glance, Case Studies
- [ ] Etapa 3 — Audience, Content
- [ ] Etapa 4 — Nodra, Why Brands, Testimonials, Contact, Footer

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

## Substituindo assets (placeholders)

- **Personagem**: `assets/characters/character-hero.svg` é o placeholder da pose do Hero. Basta substituir o arquivo (mesmo nome ou atualizando o `src` no HTML) — a proporção do container (`.hero-visual-frame`, aspect-ratio 13:16) já está definida, então a arte final só precisa respeitar esse enquadramento.
- **Logos/screenshots/depoimentos**: serão adicionados nas próximas etapas, seguindo o mesmo princípio — troca de arquivo sem alteração de layout.

## Convenções de código

- CSS organizado por seções numeradas dentro de cada arquivo (ver comentários `/* ---- N. NOME ---- */`).
- Classes seguem padrão `bloco-elemento` simples (sem metodologia BEM completa, mas consistente: ex. `.hero`, `.hero-title`, `.hero-stat`, `.hero-stat-value`).
- JS organizado em módulos IIFE independentes (`LangToggle`, `Nav`, `ScrollReveal`, `Counters`), cada um com seu próprio `init()`, inicializados uma vez em `DOMContentLoaded`. Novas seções devem seguir esse padrão.
- Animações respeitam `prefers-reduced-motion`.
