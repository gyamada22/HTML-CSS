# CSS — Flexbox e Grid

## Flexbox — container

| Propriedade | Função |
|---|---|
| `display: flex` | Ativa o Flexbox no container |
| `flex-direction` | Direção do eixo principal |
| `justify-content` | Alinhamento no eixo principal |
| `align-items` | Alinhamento no eixo cruzado |
| `flex-wrap` | Quebra de linha quando não cabe |
| `gap` | Espaçamento entre os itens |

```css
.container {
  display: flex;

  /* Direção: row (padrão) | column | row-reverse | column-reverse */
  flex-direction: row;

  /* Justify (eixo principal — horizontal quando row) */
  justify-content: flex-start;    /* padrão */
  justify-content: flex-end;
  justify-content: center;
  justify-content: space-between; /* mais usado: espaço entre os itens */
  justify-content: space-around;
  justify-content: space-evenly;

  /* Align-items (eixo cruzado — vertical quando row) */
  align-items: stretch;     /* padrão: itens ocupam altura total */
  align-items: flex-start;
  align-items: flex-end;
  align-items: center;      /* centraliza verticalmente */
  align-items: baseline;

  /* Wrap: define se os itens quebram linha */
  flex-wrap: nowrap;   /* padrão: todos na mesma linha */
  flex-wrap: wrap;     /* quebra para próxima linha se não couber */

  /* Gap: substitui margin entre itens */
  gap: 16px;           /* todos os lados */
  gap: 16px 24px;      /* row-gap | column-gap */
}

/* Padrão mais comum em navbars */
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 16px;
}

/* Centralizar um elemento na tela */
.centralizado {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
}
```

---

## Flexbox — itens

| Propriedade | Função |
|---|---|
| `flex-grow` | Cresce — quanto do espaço livre o item ocupa |
| `flex-shrink` | Encolhe — quanto o item pode diminuir quando falta espaço |
| `flex-basis` | Tamanho base — largura inicial antes de crescer ou encolher |
| `flex` | Atalho para `grow shrink basis` |
| `align-self` | Alinhamento individual — sobrescreve `align-items` do container |
| `order` | Ordem visual — sem alterar o HTML |
| `margin: auto` | Centraliza ou empurra — consome todo o espaço disponível |

```css
/* flex: grow shrink basis */
.item { flex: 0 1 auto; }   /* padrão */
.item { flex: 1; }          /* cresce para preencher: equivale a flex: 1 1 0 */
.item { flex: none; }       /* tamanho fixo: equivale a flex: 0 0 auto */

/* flex-grow: distribui o espaço livre proporcionalmente */
.sidebar  { flex: 1; }   /* ocupa 1 parte */
.conteudo { flex: 3; }   /* ocupa 3 partes (3x maior que sidebar) */

/* flex-basis: tamanho antes de crescer/encolher */
.card { flex: 1 1 200px; }  /* base de 200px, pode crescer e encolher */

/* align-self: sobrescreve align-items só para este item */
.container { align-items: center; }
.item-especial { align-self: flex-end; }

/* order: 0 é padrão, números menores aparecem antes */
.item-a { order: 2; }
.item-b { order: 1; }  /* aparece antes de item-a visualmente */
.item-c { order: 3; }

/* margin: auto — empurra elementos para as extremidades */
.logo   { margin-right: auto; }  /* empurra tudo para a direita */
.botoes { margin-left: auto; }   /* empurra para a direita no flex row */

/* Centralizar um item específico com margin auto */
.modal {
  display: flex;
  flex-direction: column;
}
.botao-fechar {
  margin-left: auto;  /* alinha o botão à direita */
}
```

---

## CSS Grid — container

| Propriedade | Função |
|---|---|
| `display: grid` | Ativa o Grid no container |
| `grid-template-columns` | Define as colunas e seus tamanhos |
| `grid-template-rows` | Define as linhas e seus tamanhos |
| `fr` | Fração — unidade proporcional do espaço disponível |
| `repeat()` | Repetição — evita escrever colunas iguais manualmente |
| `minmax()` | Flexível — define tamanho mínimo e máximo de uma trilha |
| `grid-template-areas` | Layout nomeado — mapa visual do grid em texto |
| `gap` | Espaçamento entre células |

```css
/* Grid básico: 3 colunas iguais */
.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 16px;
}

/* Mesmo resultado com repeat() */
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
}

/* Colunas de tamanhos diferentes */
.layout {
  display: grid;
  grid-template-columns: 260px 1fr;   /* sidebar fixa + conteúdo flexível */
  grid-template-rows: 64px 1fr 48px;  /* header + main + footer */
  gap: 0;
  min-height: 100vh;
}

/* fr: unidade proporcional — 2fr ocupa o dobro de 1fr */
grid-template-columns: 1fr 2fr 1fr;   /* 25% | 50% | 25% */

/* minmax(): responsivo sem media query */
grid-template-columns: repeat(3, minmax(200px, 1fr));  /* mínimo 200px, máximo 1fr */

/* auto-fill: cria quantas colunas couberem */
grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));

/* auto-fit: igual ao auto-fill mas colapsa colunas vazias (geralmente preferível) */
grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));

/* grid-template-areas: mapa visual do layout */
.pagina {
  display: grid;
  grid-template-columns: 260px 1fr;
  grid-template-rows: 64px 1fr 48px;
  grid-template-areas:
    "header  header"
    "sidebar conteudo"
    "footer  footer";
  min-height: 100vh;
}

.header   { grid-area: header; }
.sidebar  { grid-area: sidebar; }
.conteudo { grid-area: conteudo; }
.footer   { grid-area: footer; }
```

---

## CSS Grid — itens

| Propriedade | Função |
|---|---|
| `grid-column` | Posição e tamanho horizontal do item |
| `grid-row` | Posição e tamanho vertical do item |
| `span N` | Ocupa N trilhas a partir da posição atual |
| `grid-area` | Atribui o item a uma área nomeada |
| `place-self` | Alinhamento individual (atalho de `align-self` + `justify-self`) |

```css
/* Posicionamento manual: linha-início / linha-fim */
.destaque {
  grid-column: 1 / 3;   /* da coluna 1 até a 3 (ocupa 2 colunas) */
  grid-row: 1 / 2;
}

/* Span: mais legível que início/fim quando não importa a posição */
.banner {
  grid-column: span 2;  /* ocupa 2 colunas a partir de onde estiver */
  grid-row: span 1;
}

/* Ocupa a linha inteira */
.full-width {
  grid-column: 1 / -1;  /* -1 = última linha do grid */
}

/* Alinhamento individual */
.card {
  justify-self: center;  /* horizontal */
  align-self: start;     /* vertical */
  place-self: center;    /* atalho: vertical horizontal */
}
```

---

## Quando usar cada um

| | Flexbox | Grid |
|---|---|---|
| Dimensões | 1D — linha ou coluna | 2D — linha e coluna ao mesmo tempo |
| Controle | Item decide o tamanho | Container decide o tamanho |
| Ideal para | Navbars, cards em linha, botões, form rows | Layouts de página, galerias, dashboards |
| Alinhamento | Ao longo de um eixo | Em duas direções simultaneamente |

```css
/* Flexbox: componentes simples, alinhamento em uma direção */
.navbar     { display: flex; justify-content: space-between; align-items: center; }
.btn-group  { display: flex; gap: 8px; }
.form-row   { display: flex; gap: 16px; align-items: flex-end; }
.tags       { display: flex; flex-wrap: wrap; gap: 6px; }

/* Grid: estrutura de página, layouts bidimensionais */
.pagina     { display: grid; grid-template-columns: 260px 1fr; }
.galeria    { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); }
.dashboard  { display: grid; grid-template-columns: repeat(4, 1fr); gap: 16px; }

/* Juntos — padrão profissional: Grid para macro, Flex para micro */
.pagina {
  display: grid;
  grid-template-columns: 260px 1fr;
  grid-template-rows: 64px 1fr 48px;
  min-height: 100vh;
}

.navbar {           /* dentro do grid-area header */
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 24px;
}

.card-grid {        /* dentro do grid-area conteudo */
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 16px;
  padding: 24px;
}

.card {             /* dentro do card-grid */
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.card-footer {      /* dentro do card */
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: auto; /* empurra o footer para o final do card */
}
```

> **Regra prática:** se você está pensando em linha **ou** coluna → Flexbox. Se você está pensando em linha **e** coluna ao mesmo tempo → Grid. Na maioria dos projetos reais, você vai usar os dois juntos em camadas diferentes do layout.
