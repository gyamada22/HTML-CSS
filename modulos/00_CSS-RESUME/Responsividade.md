# CSS — Responsividade

## Media queries

| Sintaxe | Função |
|---|---|
| `max-width` | Até — aplica o estilo abaixo daquele tamanho |
| `min-width` | A partir de — aplica o estilo acima daquele tamanho |
| Mobile-first | Padrão atual — estilos base para mobile, media queries adicionam para telas maiores |
| Breakpoints | Pontos de quebra — tamanhos onde o layout muda |
| `orientation` | Portrait ou landscape |
| `hover` | Detecta se o dispositivo tem mouse |

```css
/* ─── Desktop-first (evitar) ─────────────────────────────── */
/* Começa com desktop e vai reduzindo */
.card { display: grid; grid-template-columns: repeat(3, 1fr); }

@media (max-width: 768px) {
  .card { grid-template-columns: 1fr; }   /* sobrescreve para mobile */
}

/* ─── Mobile-first (padrão atual) ────────────────────────── */
/* Começa com mobile e vai adicionando conforme a tela cresce */
.card { display: grid; grid-template-columns: 1fr; }   /* base: mobile */

@media (min-width: 640px) {
  .card { grid-template-columns: repeat(2, 1fr); }     /* tablet pequeno */
}

@media (min-width: 1024px) {
  .card { grid-template-columns: repeat(3, 1fr); }     /* desktop */
}
```

### Breakpoints

| Nome | Tamanho | Dispositivo típico |
|---|---|---|
| sm | `640px` | Mobile grande / landscape |
| md | `768px` | Tablet |
| lg | `1024px` | Tablet grande / laptop |
| xl | `1280px` | Desktop |

> Esses são os mesmos breakpoints do Tailwind CSS — aprender eles agora facilita a migração quando você chegar no Tailwind.

```css
/* Sistema de breakpoints mobile-first */
/* base          → mobile (< 640px) */
/* min-width: 640px  → sm  */
/* min-width: 768px  → md  */
/* min-width: 1024px → lg  */
/* min-width: 1280px → xl  */

.titulo {
  font-size: 1.5rem;       /* mobile */
}
@media (min-width: 768px) {
  .titulo { font-size: 2rem; }    /* tablet */
}
@media (min-width: 1024px) {
  .titulo { font-size: 2.5rem; }  /* desktop */
}

/* Alternativa moderna: clamp() elimina media queries para tipografia */
.titulo {
  font-size: clamp(1.5rem, 4vw, 2.5rem);
  /* mínimo 1.5rem → escala com a tela → máximo 2.5rem */
}
```

### Media queries extras

```css
/* Orientação do dispositivo */
@media (orientation: portrait) {
  /* tela mais alta do que larga (mobile em pé) */
}
@media (orientation: landscape) {
  /* tela mais larga do que alta (mobile deitado, desktop) */
}

/* Hover: detecta se o dispositivo tem mouse */
@media (hover: hover) {
  /* o dispositivo suporta hover (mouse/trackpad) */
  .btn:hover { background: #534AB7; }
}
@media (hover: none) {
  /* touch — não depende de hover para mostrar conteúdo importante */
  .tooltip { display: none; }
}

/* Dark mode */
@media (prefers-color-scheme: dark) {
  :root {
    --cor-fundo: #121212;
    --cor-texto: #e8e8e8;
  }
}

/* Redução de movimento (acessibilidade) */
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}

/* Combinando condições */
@media (min-width: 768px) and (max-width: 1023px) {
  /* apenas tablets */
}
```

---

## Container queries

| Sintaxe | Função |
|---|---|
| `@container` | Aplica estilos baseado no tamanho do container pai, não da tela |
| `container-type` | Ativa o contexto de container no elemento pai |
| `container-name` | Nome opcional para referenciar um container específico |
| `cqw` / `cqh` | Unidades relativas ao container (container query width/height) |

```css
/*
  Diferença fundamental:

  @media   → reage ao tamanho da JANELA (viewport)
  @container → reage ao tamanho do CONTAINER PAI do componente

  Vantagem: o mesmo componente se adapta em qualquer contexto,
  independente de onde estiver na página.
*/

/* 1. Ativa o container no pai */
.card-wrapper {
  container-type: inline-size;   /* monitora a largura */
  container-name: card;          /* nome opcional */
}

/* 2. O componente filho se adapta ao container */
.card {
  display: flex;
  flex-direction: column;        /* base: layout vertical (container pequeno) */
}

@container (min-width: 400px) {
  .card {
    flex-direction: row;         /* layout horizontal quando o container crescer */
  }
}

@container (min-width: 600px) {
  .card-titulo {
    font-size: 1.5rem;
  }
}

/* Com nome: reage a um container específico */
@container card (min-width: 500px) {
  .card-imagem { width: 40%; }
}

/* Unidades cq: relativas ao container (não à viewport) */
.card-titulo {
  font-size: clamp(1rem, 5cqw, 1.5rem);
  /* 5% da largura do container, entre 1rem e 1.5rem */
}

/* Exemplo real: sidebar vs conteúdo principal */
.sidebar .card-wrapper    { container-type: inline-size; }
.conteudo-main .card-wrapper { container-type: inline-size; }

/* O mesmo .card se comporta diferente em cada contexto */
@container (min-width: 300px) { .card { flex-direction: row; } }

/*
  Na sidebar (container ~260px): layout vertical
  No conteúdo principal (container ~800px): layout horizontal
  — sem nenhuma media query específica por contexto
*/
```

> **Por que preferir container queries em UI moderna:** com `@media`, você precisa saber onde o componente vai estar na página para escrever os breakpoints certos. Com `@container`, o componente se adapta sozinho ao espaço disponível — funciona em qualquer contexto sem ajuste.

---

## Imagens responsivas no CSS

| Propriedade | Função |
|---|---|
| `object-fit` | Comportamento da imagem dentro do seu container |
| `cover` | Preenche — corta as bordas para cobrir o container sem distorcer |
| `contain` | Ajusta — imagem inteira visível, pode sobrar espaço nas bordas |
| `aspect-ratio` | Proporção — mantém a relação largura/altura fixa |
| `background-size` | Controla o tamanho de imagens de fundo |

```css
/* object-fit: controla imagens dentro de um container com tamanho fixo */
.thumbnail {
  width: 100%;
  height: 200px;
  object-fit: cover;        /* preenche sem distorcer, corta bordas */
  object-position: center;  /* centro do corte (padrão) */
  object-position: top;     /* rostos: manter o topo visível */
}

/* Valores de object-fit */
img { object-fit: fill; }     /* padrão: estica e distorce */
img { object-fit: cover; }    /* preenche e corta — mais usado */
img { object-fit: contain; }  /* mostra tudo, pode sobrar espaço */
img { object-fit: none; }     /* tamanho original, sem escalar */
img { object-fit: scale-down; }  /* contain mas nunca aumenta */

/* aspect-ratio: mantém proporção sem altura fixa */
.video-wrapper {
  width: 100%;
  aspect-ratio: 16 / 9;     /* sempre 16:9 independente da largura */
}

.avatar {
  width: 48px;
  aspect-ratio: 1;           /* quadrado */
  border-radius: 50%;        /* círculo */
  object-fit: cover;
}

.card-imagem {
  width: 100%;
  aspect-ratio: 4 / 3;
  object-fit: cover;
}

/* background-size para imagens de fundo */
.hero {
  background-image: url('hero.jpg');
  background-size: cover;      /* preenche — mais comum */
  background-size: contain;    /* imagem inteira visível */
  background-size: 100% auto;  /* largura 100%, altura proporcional */
  background-position: center;
  background-repeat: no-repeat;
  min-height: 400px;
}

/* Shorthand */
.hero {
  background: url('hero.jpg') center / cover no-repeat;
}

/* Imagem de fundo responsiva com múltiplas resoluções */
.hero {
  background-image: url('hero-mobile.jpg');
}
@media (min-width: 768px) {
  .hero {
    background-image: url('hero-desktop.jpg');
  }
}
```

> **Dica:** sempre defina `width`, `height` e `aspect-ratio` em imagens — evita o layout shift (CLS) que derruba a nota de performance do Google. Com `aspect-ratio`, o navegador reserva o espaço antes da imagem carregar.
