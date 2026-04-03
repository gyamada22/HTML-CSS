# HTML — Estrutura e Semântica

## Estrutura do documento

| Tag / Conceito | Função |
|---|---|
| `<!DOCTYPE html>` | Tipo do documento — informa ao navegador que é HTML5 |
| `<html>` | Raiz — envolve todo o conteúdo da página |
| `<head>` | Configurações invisíveis — meta dados, links, scripts |
| `<body>` | Conteúdo visível — tudo que o usuário vê |
| `charset="UTF-8"` | Acentos funcionam — codificação de caracteres |
| `viewport` | Responsivo — controla escala em dispositivos móveis |
| `<title>` | Nome da aba — aparece no título do navegador |
| `<meta name="description">` | SEO — descrição exibida nos resultados de busca |

```html
<!DOCTYPE html>
<html lang="pt-BR">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" content="Descrição da página para SEO" />
    <title>Nome da aba</title>
  </head>
  <body>
    <!-- conteúdo visível aqui -->
  </body>
</html>
```

---

## Tags semânticas de seção

| Tag | Função |
|---|---|
| `<header>` | Topo — cabeçalho da página ou de uma seção |
| `<main>` | Conteúdo principal — único por página |
| `<footer>` | Rodapé — informações finais, links, créditos |
| `<nav>` | Navegação — menus e links de navegação |
| `<section>` | Divisão por tema — agrupa conteúdo relacionado |
| `<article>` | Conteúdo independente — post, card, notícia |
| `<aside>` | Lateral / complemento — sidebar, notas extras |
| `<h1>`–`<h6>` | Hierarquia de títulos — h1 é o mais importante |

```html
<header>
  <nav>...</nav>
</header>

<main>
  <section>
    <article>...</article>
  </section>
  <aside>...</aside>
</main>

<footer>...</footer>
```

> **Dica:** use apenas um `<h1>` por página. A hierarquia (h1 > h2 > h3) afeta SEO e acessibilidade.

---

## Tags de conteúdo

| Tag | Função |
|---|---|
| `<p>` | Parágrafo |
| `<span>` | Texto pequeno inline — sem quebra de linha |
| `<div>` | Container genérico — sem significado semântico |
| `<strong>` | Importância — negrito com significado |
| `<em>` | Ênfase — itálico com significado |
| `<small>` | Texto menor — notas, avisos legais |
| `<blockquote>` | Citação longa — trecho de outra fonte |
| `<cite>` | Fonte — nome da obra ou autor citado |
| `<code>` | Código — trecho de código inline |
| `<pre>` | Mantém formatação — espaços e quebras de linha |
| `<br>` | Quebra de linha |
| `<hr>` | Linha separadora — divisão temática |
| `<time>` | Data / tempo — semântico para máquinas |
| `<address>` | Contato — endereço ou e-mail do autor |

```html
<p>Texto com <strong>palavra importante</strong> e <em>ênfase</em>.</p>

<blockquote>
  <p>"Frase citada de outra fonte."</p>
  <cite>Nome do Autor</cite>
</blockquote>

<pre><code>
function hello() {
  console.log("olá");
}
</code></pre>

<time datetime="2026-01-15">15 de janeiro de 2026</time>
```

---

## Listas

| Tag | Função |
|---|---|
| `<ul>` | Lista não ordenada — marcadores (bolinhas) |
| `<ol>` | Lista ordenada — numerada |
| `<li>` | Item da lista |
| Lista aninhada | Lista dentro de outra — menus, categorias |
| `<dl>` | Lista de definição |
| `<dt>` | Termo da definição |
| `<dd>` | Descrição do termo |

```html
<!-- Lista não ordenada -->
<ul>
  <li>HTML</li>
  <li>CSS
    <ul>
      <li>Flexbox</li>
      <li>Grid</li>
    </ul>
  </li>
</ul>

<!-- Lista ordenada -->
<ol>
  <li>Primeiro passo</li>
  <li>Segundo passo</li>
</ol>

<!-- Lista de definição -->
<dl>
  <dt>HTML</dt>
  <dd>Linguagem de marcação para estrutura de páginas web.</dd>
</dl>
```

---

## Links e navegação

| Atributo / Tag | Função |
|---|---|
| `<a>` | Cria link — elemento âncora |
| `href` absoluto | Link externo — URL completa com https:// |
| `href` relativo | Link interno — caminho relativo ao arquivo atual |
| `target="_blank"` | Abre em nova aba |
| `rel="noopener noreferrer"` | Segurança — evita acesso à página de origem |
| `#id` | Navegação dentro da página — âncora interna |
| `download` | Força download do arquivo linkado |

```html
<!-- Link externo seguro -->
<a href="https://example.com" target="_blank" rel="noopener noreferrer">
  Visitar site
</a>

<!-- Link interno relativo -->
<a href="/sobre">Sobre nós</a>

<!-- Âncora interna -->
<a href="#contato">Ir para contato</a>
<section id="contato">...</section>

<!-- Download -->
<a href="/files/curriculo.pdf" download>Baixar currículo</a>
```

---

## Imagens e mídia

| Tag / Atributo | Função |
|---|---|
| `<img src="">` | Imagem |
| `alt` | Descrição — acessibilidade e SEO (obrigatório) |
| `width` / `height` | Evita layout quebrando durante carregamento |
| `srcset` / `sizes` | Imagens responsivas — diferentes resoluções |
| `<picture>` / `<source>` | Controle avançado — formatos e breakpoints |
| `<figure>` / `<figcaption>` | Imagem + legenda semântica |
| `<video>` | Vídeo com controles nativos |
| `<audio>` | Áudio |
| `loading="lazy"` | Carrega só quando entra na viewport |

```html
<!-- Imagem básica -->
<img src="foto.jpg" alt="Descrição da imagem" width="800" height="600" loading="lazy" />

<!-- Imagem responsiva -->
<img
  src="foto-800.jpg"
  srcset="foto-400.jpg 400w, foto-800.jpg 800w, foto-1200.jpg 1200w"
  sizes="(max-width: 600px) 400px, 800px"
  alt="Descrição"
/>

<!-- Controle avançado de formato -->
<picture>
  <source srcset="foto.avif" type="image/avif" />
  <source srcset="foto.webp" type="image/webp" />
  <img src="foto.jpg" alt="Descrição" />
</picture>

<!-- Imagem com legenda -->
<figure>
  <img src="grafico.png" alt="Gráfico de vendas 2026" />
  <figcaption>Crescimento de vendas no primeiro semestre de 2026.</figcaption>
</figure>

<!-- Vídeo -->
<video controls width="640" poster="thumbnail.jpg">
  <source src="video.mp4" type="video/mp4" />
  Seu navegador não suporta vídeo.
</video>

<!-- Áudio -->
<audio controls>
  <source src="audio.mp3" type="audio/mpeg" />
</audio>
```
