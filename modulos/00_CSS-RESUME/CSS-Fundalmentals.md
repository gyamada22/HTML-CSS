# CSS — Fundamentos

## Como o CSS funciona

| Conceito | Função |
|---|---|
| Cascata | Decide quem ganha — quando duas regras conflitam, o CSS tem critérios de desempate |
| Herança | Pai → filho — propriedades como `color` e `font-size` se propagam automaticamente |
| Especificidade | Força do seletor — quanto mais específico, mais peso tem a regra |
| Ordem | Último vence — entre regras de mesma especificidade, a que vem depois prevalece |
| `!important` | Sobrescreve tudo — evitar; quebra a cascata e dificulta manutenção |

```css
/* Especificidade: ID (1,0,0) > classe (0,1,0) > tag (0,0,1) */

p { color: gray; }              /* especificidade: 0,0,1 */
.texto { color: blue; }         /* especificidade: 0,1,0 */
#titulo { color: red; }         /* especificidade: 1,0,0 */

/* Ordem: a segunda regra vence por vir depois (mesma especificidade) */
.card { background: white; }
.card { background: #f5f5f5; }  /* esta vence */

/* Herança: color e font-* herdam, margin e padding NÃO herdam */
body { color: #333; font-family: sans-serif; }  /* todos os filhos herdam */

/* Forçar herança de propriedade que não herda naturalmente */
.filho { border: inherit; }

/* !important: só use como último recurso (ex: sobrescrever CSS de terceiros) */
.urgente { color: red !important; }
```

> **Regra de ouro da especificidade:** inline style > ID > classe/pseudo-classe/atributo > tag. Calcule como um número de 3 dígitos: `(IDs, classes, tags)`. Ex: `#nav .link:hover` = `(1,2,0)`.

---

## Seletores

| Seletor | Sintaxe | Função |
|---|---|---|
| Tag | `p` | Seleciona todos os elementos daquela tag |
| Classe | `.card` | Seleciona todos com aquela classe |
| ID | `#titulo` | Seleciona o elemento com aquele ID único |
| Descendente | `nav a` | Seleciona `a` dentro de `nav` (qualquer nível) |
| Filho direto | `ul > li` | Seleciona `li` filho imediato de `ul` |
| Irmão adjacente | `h2 + p` | Seleciona o `p` que vem imediatamente após `h2` |
| Atributo | `[type="email"]` | Seleciona elementos com aquele atributo e valor |
| Negação | `:not(.ativo)` | Seleciona todos que NÃO têm aquela classe |

```css
/* Tag, classe, ID */
p { }
.destaque { }
#header { }

/* Descendente vs filho direto */
nav a { }          /* qualquer <a> dentro de <nav>, em qualquer nível */
ul > li { }        /* apenas <li> filhos diretos de <ul> */

/* Irmão adjacente */
h2 + p { margin-top: 0; }   /* parágrafo logo após um h2 */

/* Atributo */
[disabled] { opacity: 0.5; }
[type="email"] { border-color: blue; }
[href^="https"] { }   /* href que começa com https */
[href$=".pdf"] { }    /* href que termina com .pdf */
[class*="btn"] { }    /* class que contém "btn" */

/* Negação */
li:not(:last-child) { border-bottom: 1px solid #eee; }
input:not([disabled]) { background: white; }

/* Múltiplos seletores com a mesma regra */
h1, h2, h3 { font-family: serif; }
```

---

## Pseudo-classes

### Interação

| Pseudo-classe | Função |
|---|---|
| `:hover` | Mouse sobre o elemento |
| `:focus` | Elemento com foco (teclado ou clique) |
| `:focus-visible` | Foco via teclado apenas — não dispara no clique com mouse |
| `:active` | Elemento sendo clicado |
| `:visited` | Link já visitado |

```css
a:hover  { color: blue; }
button:focus-visible { outline: 2px solid #534AB7; }  /* preferir ao :focus para botões */
button:active { transform: scale(0.98); }
a:visited { color: purple; }
```

### Estrutura

| Pseudo-classe | Função |
|---|---|
| `:first-child` | Primeiro filho do pai |
| `:last-child` | Último filho do pai |
| `:nth-child(n)` | Filho de posição específica |
| `:nth-child(odd/even)` | Ímpares ou pares |
| `:only-child` | Filho único |
| `:first-of-type` | Primeiro elemento daquele tipo |

```css
li:first-child { font-weight: 500; }
li:last-child  { border-bottom: none; }
tr:nth-child(even) { background: #f9f9f9; }   /* linhas pares da tabela */
tr:nth-child(3n)   { }                         /* a cada 3 linhas */
p:only-child { margin: 0; }
```

### Formulários

| Pseudo-classe | Função |
|---|---|
| `:checked` | Checkbox ou radio marcado |
| `:disabled` | Campo desabilitado |
| `:required` | Campo obrigatório |
| `:valid` | Campo com valor válido |
| `:invalid` | Campo com valor inválido |
| `:placeholder-shown` | Campo mostrando o placeholder |

```css
input:disabled   { opacity: 0.5; cursor: not-allowed; }
input:required   { border-left: 3px solid red; }
input:valid      { border-color: green; }
input:invalid    { border-color: red; }

/* Só mostra erro após o usuário interagir, não no carregamento */
input:not(:placeholder-shown):invalid { border-color: red; }
```

### Pseudo-classes modernas

| Pseudo-classe | Função |
|---|---|
| `:is()` | Agrupa seletores — reduz repetição |
| `:where()` | Igual ao `:is()` mas especificidade zero |
| `:has()` | Seletor pai — seleciona elemento que contém outro |

```css
/* :is() — substitui listas longas de seletores */
:is(h1, h2, h3, h4) { line-height: 1.2; }

/* Sem :is() seria: */
h1, h2, h3, h4 { line-height: 1.2; }

/* :where() — mesmo resultado mas sem adicionar especificidade (ótimo para resets) */
:where(h1, h2, h3) { margin: 0; }

/* :has() — o "seletor pai" que o CSS nunca teve */
form:has(input:invalid) { border-color: red; }       /* form com input inválido */
.card:has(img) { padding: 0; }                       /* card que contém imagem */
li:has(ul) { font-weight: 500; }                     /* item de lista com sublista */
label:has(+ input:required)::after { content: " *"; } /* label cujo input é required */
```

---

## Pseudo-elementos

| Pseudo-elemento | Função |
|---|---|
| `::before` | Insere conteúdo antes do elemento (via `content`) |
| `::after` | Insere conteúdo depois do elemento (via `content`) |
| `::placeholder` | Estiliza o texto placeholder de inputs |
| `::selection` | Estiliza o texto selecionado pelo usuário |
| `::first-line` | Estiliza apenas a primeira linha de um parágrafo |
| `::first-letter` | Estiliza apenas a primeira letra |

```css
/* before/after: sempre precisam de content (pode ser vazio) */
.card::before {
  content: '';
  display: block;
  height: 4px;
  background: #534AB7;
  border-radius: 4px 4px 0 0;
}

.link-externo::after {
  content: ' ↗';
  font-size: 0.8em;
}

/* Contador automático com pseudo-elementos */
.lista { counter-reset: item; }
.lista li::before {
  counter-increment: item;
  content: counter(item) ". ";
  font-weight: 500;
}

/* Placeholder */
::placeholder { color: #aaa; font-style: italic; }
input:focus::placeholder { opacity: 0; }  /* some o placeholder no foco */

/* Selection */
::selection { background: #EEEDFE; color: #26215C; }

/* First-line e first-letter */
p::first-line   { font-weight: 500; }
p::first-letter { font-size: 2em; float: left; margin-right: 4px; }
```

---

## Box model

| Propriedade | Função |
|---|---|
| `margin` | Fora — espaço externo, entre elementos |
| `padding` | Dentro — espaço interno, entre conteúdo e borda |
| `border` | Borda — linha entre padding e margin |
| `box-sizing: border-box` | Controle total — width inclui padding e border |
| `overflow` | Comportamento do conteúdo que ultrapassa o container |

```css
/*
  Box model padrão (content-box):
  largura total = width + padding + border

  Box model recomendado (border-box):
  largura total = width (padding e border ficam dentro)
*/

/* Reset global: sempre aplique no início do CSS */
*, *::before, *::after {
  box-sizing: border-box;
}

.card {
  width: 300px;         /* com border-box: 300px é o total */
  padding: 16px 24px;   /* top/bottom: 16px | left/right: 24px */
  border: 1px solid #eee;
  margin-bottom: 16px;
}

/* Margin: shorthand top | right | bottom | left */
margin: 8px 16px 8px 16px;
margin: 8px 16px;       /* top/bottom | left/right */
margin: 8px;            /* todos os lados */
margin: 0 auto;         /* centraliza horizontalmente (precisa de width) */

/* Margin collapse: margens verticais de irmãos se sobrepõem (não somam) */
.paragrafo-1 { margin-bottom: 24px; }
.paragrafo-2 { margin-top: 16px; }
/* espaço entre eles = 24px (o maior), não 40px */

/* Overflow */
overflow: visible;  /* padrão — conteúdo vaza para fora */
overflow: hidden;   /* corta o conteúdo que excede */
overflow: scroll;   /* sempre mostra scrollbar */
overflow: auto;     /* scrollbar só quando necessário (preferir) */
overflow-x: hidden; overflow-y: auto;  /* controle por eixo */

/* outline: parecido com border mas não ocupa espaço no layout */
button:focus-visible { outline: 2px solid #534AB7; outline-offset: 2px; }
```

> **Dica:** adicione `box-sizing: border-box` globalmente logo no início do seu CSS. É a primeira coisa que todo projeto profissional faz — sem isso, calcular larguras com padding vira pesadelo.

---

## Variáveis CSS

| Sintaxe | Função |
|---|---|
| `--minha-var: valor` | Cria a variável — nome começa obrigatoriamente com `--` |
| `var(--minha-var)` | Usa a variável |
| `var(--var, fallback)` | Fallback de segurança — valor usado se a variável não existir |
| `:root` | Escopo global — variáveis definidas aqui ficam disponíveis em toda a página |

```css
/* Definição global em :root */
:root {
  --cor-primaria: #534AB7;
  --cor-texto: #1a1a1a;
  --cor-fundo: #ffffff;
  --espacamento-base: 16px;
  --raio-borda: 8px;
  --fonte-titulo: 'Inter', sans-serif;
}

/* Uso */
.botao {
  background: var(--cor-primaria);
  color: var(--cor-fundo);
  padding: var(--espacamento-base);
  border-radius: var(--raio-borda);
}

/* Fallback: se --cor-destaque não existir, usa #e74c3c */
.alerta {
  color: var(--cor-destaque, #e74c3c);
}

/* Variáveis locais: definidas no componente, sobrescrevem as globais */
.card {
  --raio-borda: 4px;   /* só para cards */
  border-radius: var(--raio-borda);
}

/* Variáveis em media queries */
@media (max-width: 768px) {
  :root {
    --espacamento-base: 12px;
    --fonte-tamanho: 15px;
  }
}

/* Tema dark mode com variáveis */
:root {
  --cor-fundo: #ffffff;
  --cor-texto: #1a1a1a;
  --cor-superficie: #f5f5f5;
}

@media (prefers-color-scheme: dark) {
  :root {
    --cor-fundo: #121212;
    --cor-texto: #e8e8e8;
    --cor-superficie: #1e1e1e;
  }
}

/* Todos os componentes usam as variáveis — o tema muda automaticamente */
body {
  background: var(--cor-fundo);
  color: var(--cor-texto);
}

.card {
  background: var(--cor-superficie);
}

/* Variáveis manipuladas via JavaScript */
document.documentElement.style.setProperty('--cor-primaria', '#D85A30');
```

> **Dica:** crie todas as cores, espaçamentos e tamanhos como variáveis em `:root` desde o início do projeto. Quando precisar trocar o tema ou ajustar o design, você muda em um lugar só — não em 50 arquivos diferentes.
