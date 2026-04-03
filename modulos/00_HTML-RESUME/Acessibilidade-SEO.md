# HTML — Acessibilidade, SEO e Atributos Globais

## Acessibilidade básica

| Tag / Atributo | Função |
|---|---|
| `alt` | Descrição da imagem — lida por leitores de tela e exibida se a imagem falhar |
| `h1`–`h6` | Estrutura de headings — define a hierarquia do conteúdo para navegação assistiva |
| `tabindex` | Navegação por teclado — controla a ordem do foco via Tab |
| Foco visível | Indicador visual de qual elemento está focado — essencial para usuários de teclado |
| `aria-*` | Acessibilidade extra — descreve comportamento e estado para leitores de tela |
| Skip link | Navegação rápida — link oculto que pula direto para o conteúdo principal |

```html
<!-- Alt descritivo (descreva o que a imagem comunica, não o que ela é) -->
<img src="grafico.png" alt="Gráfico mostrando crescimento de 40% nas vendas em 2026" />

<!-- Imagem decorativa: alt vazio para o leitor de tela ignorar -->
<img src="divisor.png" alt="" />

<!-- Hierarquia de headings: apenas um h1 por página -->
<h1>Título principal da página</h1>
  <h2>Seção</h2>
    <h3>Subseção</h3>

<!-- Tabindex: 0 = ordem natural do DOM, -1 = focável só via JS, >0 = evitar -->
<div tabindex="0">Elemento focável pelo teclado</div>
<div tabindex="-1" id="modal">Focável apenas por JS</div>

<!-- Foco visível: nunca remova o outline sem substituir por outro estilo -->
<style>
  :focus-visible {
    outline: 2px solid #534AB7;
    outline-offset: 2px;
  }
</style>

<!-- ARIA: descreve elementos que o HTML sozinho não consegue -->
<button aria-label="Fechar modal">X</button>
<nav aria-label="Menu principal">...</nav>
<div role="alert" aria-live="polite">Mensagem de erro ao vivo</div>
<button aria-expanded="false" aria-controls="menu">Abrir menu</button>
<input aria-describedby="dica-senha" type="password" />
<p id="dica-senha">Mínimo 8 caracteres com letras e números</p>

<!-- aria-hidden: esconde elemento decorativo do leitor de tela -->
<span aria-hidden="true">★★★★☆</span>
<span class="sr-only">4 de 5 estrelas</span>

<!-- Skip link: aparece só no foco, pula para o conteúdo principal -->
<a href="#conteudo" class="skip-link">Pular para o conteúdo</a>
<main id="conteudo">...</main>

<style>
  .skip-link {
    position: absolute;
    top: -100%;
  }
  .skip-link:focus {
    top: 0;
  }

  /* Classe utilitária: visível para leitores de tela, invisível visualmente */
  .sr-only {
    position: absolute;
    width: 1px;
    height: 1px;
    overflow: hidden;
    clip: rect(0, 0, 0, 0);
    white-space: nowrap;
  }
</style>
```

> **Dica:** teste sua página navegando só com Tab e Enter, sem usar o mouse. Se você conseguir usar tudo — menus, formulários, modais — sua acessibilidade está boa.

---

## SEO básico no HTML

| Tag / Atributo | Função |
|---|---|
| `<meta name="description">` | Resumo no Google — aparece embaixo do título nos resultados de busca |
| `og:*` | Preview social — controla como a página aparece no WhatsApp, Twitter, LinkedIn |
| `<link rel="canonical">` | Evita duplicação — diz ao Google qual é a URL principal |
| `lang` | Idioma — indica o idioma da página para buscadores e leitores de tela |
| `<h1>` | Título principal — único por página, define o tema do conteúdo |
| Structured data | Entendimento do Google — dados estruturados em JSON-LD para rich results |

```html
<html lang="pt-BR">
<head>

  <!-- Description: entre 120–160 caracteres -->
  <meta name="description" content="Aprenda HTML do zero com exemplos práticos e projetos reais para iniciantes em 2026." />

  <!-- Canonical: sempre aponte para a URL preferida -->
  <link rel="canonical" href="https://meusite.com/html-para-iniciantes" />

  <!-- Open Graph: preview no WhatsApp, LinkedIn, Facebook -->
  <meta property="og:title"       content="HTML para Iniciantes — Guia 2026" />
  <meta property="og:description" content="Aprenda HTML do zero com exemplos práticos." />
  <meta property="og:image"       content="https://meusite.com/og-html.png" />
  <meta property="og:url"         content="https://meusite.com/html-para-iniciantes" />
  <meta property="og:type"        content="article" />

  <!-- Twitter Card -->
  <meta name="twitter:card"        content="summary_large_image" />
  <meta name="twitter:title"       content="HTML para Iniciantes — Guia 2026" />
  <meta name="twitter:description" content="Aprenda HTML do zero com exemplos práticos." />
  <meta name="twitter:image"       content="https://meusite.com/og-html.png" />

  <!-- Structured data: artigo em JSON-LD -->
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "Article",
    "headline": "HTML para Iniciantes — Guia 2026",
    "author": { "@type": "Person", "name": "Seu Nome" },
    "datePublished": "2026-01-15"
  }
  </script>

</head>
<body>
  <h1>HTML para Iniciantes — Guia 2026</h1>
</body>
```

> **Dica:** a imagem `og:image` deve ter no mínimo 1200×630px. É ela que aparece no preview quando alguém compartilha seu link no WhatsApp ou LinkedIn.

---

## Performance e `<head>`

| Tag / Atributo | Função |
|---|---|
| `rel="preload"` | Prioridade alta — carrega recurso crítico antes do parser chegar nele |
| `rel="prefetch"` | Próxima página — baixa em segundo plano para navegação futura |
| `async` | Otimiza JS — baixa em paralelo, executa assim que pronto (sem ordem garantida) |
| `defer` | Otimiza JS — baixa em paralelo, executa só após o HTML ser parseado (com ordem) |
| Favicon | Ícone — aparece na aba do navegador e favoritos |
| `manifest.json` | App — permite instalar o site como PWA |
| `<script>` no final | Mais rápido — não bloqueia o parsing do HTML |

```html
<head>

  <!-- Preload: use para fontes, CSS crítico e imagens hero -->
  <link rel="preload" href="/fonts/inter.woff2" as="font" type="font/woff2" crossorigin />
  <link rel="preload" href="/css/critical.css" as="style" />

  <!-- Prefetch: use para páginas que o usuário provavelmente vai acessar -->
  <link rel="prefetch" href="/sobre" />

  <!-- Favicon -->
  <link rel="icon" href="/favicon.ico" sizes="any" />
  <link rel="icon" href="/favicon.svg" type="image/svg+xml" />
  <link rel="apple-touch-icon" href="/apple-touch-icon.png" />

  <!-- PWA manifest -->
  <link rel="manifest" href="/manifest.json" />

  <!-- async: scripts independentes (analytics, chat widget) -->
  <script async src="https://analytics.example.com/script.js"></script>

  <!-- defer: scripts que dependem do DOM pronto -->
  <script defer src="/js/app.js"></script>

</head>
<body>

  <!-- Conteúdo da página -->

  <!-- Script sem async/defer: coloque no final do body como último recurso -->
  <script src="/js/legado.js"></script>
</body>
```

> **Diferença entre `async` e `defer`:** use `defer` para seus próprios scripts (mantém a ordem de execução e espera o DOM). Use `async` para scripts de terceiros independentes, como Google Analytics.

---

## Atributos globais

| Atributo | Função |
|---|---|
| `id` | Único — identifica um elemento específico na página |
| `class` | Reutilizável — aplica estilos e comportamentos a múltiplos elementos |
| `data-*` | Dados extras — armazena informações customizadas acessíveis via JS |
| `style` | CSS inline — evitar; dificulta manutenção e sobrescreve folhas de estilo |
| `hidden` | Esconder — remove o elemento do layout e da árvore de acessibilidade |
| `contenteditable` | Editar — permite ao usuário editar o conteúdo diretamente no navegador |
| `draggable` | Arrastar — habilita drag and drop nativo |

```html
<!-- id: único por página, use para âncoras, labels e JS -->
<section id="sobre">...</section>
<a href="#sobre">Ir para sobre</a>

<!-- class: reutilizável, use para estilos e comportamentos -->
<div class="card destaque">...</div>
<div class="card">...</div>

<!-- data-*: atributos customizados acessados via JS -->
<button data-id="42" data-acao="deletar">Deletar</button>

<script>
  const btn = document.querySelector('button');
  console.log(btn.dataset.id);    // "42"
  console.log(btn.dataset.acao);  // "deletar"
</script>

<!-- style inline: evitar — só use para valores dinâmicos via JS -->
<div style="--progresso: 75%">...</div>  <!-- variável CSS dinâmica: ok -->
<p style="color: red">Evitar isso</p>    <!-- estilo fixo: mover para CSS -->

<!-- hidden: esconde semanticamente (diferente de display:none via CSS) -->
<div hidden>Não aparece e não é lido por leitores de tela</div>

<!-- contenteditable: áreas editáveis sem input (editores de texto, notas) -->
<div contenteditable="true" role="textbox" aria-label="Anotações">
  Clique para editar...
</div>

<!-- draggable: habilita o evento drag nativo -->
<div draggable="true" ondragstart="iniciarArraste(event)">
  Arraste este card
</div>
```

> **Dica:** `data-*` é a ponte oficial entre HTML e JavaScript — é a forma correta de guardar informações em elementos sem usar variáveis globais ou IDs forçados. Quando você aprender JS, vai usar muito `dataset`.
