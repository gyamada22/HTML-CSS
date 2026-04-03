# HTML — Formulários e Tabelas

## Estrutura de formulários

| Tag / Atributo | Função |
|---|---|
| `<form>` | Container — envolve todos os campos do formulário |
| `action` | Destino — URL para onde os dados são enviados |
| `method` | GET ou POST — como os dados são enviados |
| `<label for="">` | Conecta com o input pelo `id` — acessibilidade obrigatória |
| `<input id="">` | Campo de entrada — recebe dados do usuário |
| `<fieldset>` | Agrupa campos relacionados |
| `<legend>` | Título do grupo — aparece na borda do fieldset |
| `placeholder` | Dica dentro do campo — não substitui `<label>` |
| `autocomplete` | Preenchimento automático pelo navegador |

```html
<form action="/contato" method="POST">

  <fieldset>
    <legend>Dados pessoais</legend>

    <label for="nome">Nome</label>
    <input type="text" id="nome" name="nome" placeholder="Seu nome completo" autocomplete="name" />

    <label for="email">E-mail</label>
    <input type="email" id="email" name="email" placeholder="seu@email.com" autocomplete="email" />
  </fieldset>

  <button type="submit">Enviar</button>

</form>
```

> **Dica:** `placeholder` desaparece quando o usuário digita — sempre use `<label>` para descrever o campo. Sem label, leitores de tela não conseguem identificar o campo.

---

## Tipos de input

| Tipo | Função |
|---|---|
| `type="text"` | Texto livre |
| `type="email"` | Valida formato de e-mail automaticamente |
| `type="password"` | Texto escondido com asteriscos |
| `type="number"` | Aceita apenas números |
| `type="tel"` | Telefone — abre teclado numérico no mobile |
| `type="url"` | Link — valida formato de URL |
| `type="date"` | Seletor de data |
| `type="time"` | Seletor de hora |
| `type="checkbox"` | Múltipla escolha — pode marcar vários |
| `type="radio"` | Escolha única — mesmo `name` agrupa as opções |
| `type="range"` | Slider — valor numérico arrastável |
| `type="color"` | Seletor de cor |
| `type="file"` | Upload de arquivo |
| `type="hidden"` | Invisível — envia dados sem o usuário ver |

```html
<!-- Texto e dados -->
<input type="text"     name="nome" />
<input type="email"    name="email" />
<input type="password" name="senha" />
<input type="number"   name="idade" />
<input type="tel"      name="telefone" />
<input type="url"      name="site" />
<input type="date"     name="nascimento" />
<input type="time"     name="horario" />

<!-- Seleção -->
<input type="checkbox" name="termos" id="termos" />
<label for="termos">Aceito os termos</label>

<input type="radio" name="plano" id="basico" value="basico" />
<label for="basico">Básico</label>
<input type="radio" name="plano" id="pro" value="pro" />
<label for="pro">Pro</label>

<!-- Outros -->
<input type="range" name="volume" min="0" max="100" value="50" />
<input type="color" name="cor" value="#534AB7" />
<input type="file"  name="foto" accept="image/*" />
<input type="hidden" name="token" value="abc123" />
```

---

## Validação nativa HTML

| Atributo | Função |
|---|---|
| `required` | Campo obrigatório — não envia o form se vazio |
| `min` / `max` | Limite de valor numérico ou data |
| `minlength` / `maxlength` | Limite de caracteres em texto |
| `pattern` | Validação personalizada via regex |
| `type` | Valida automaticamente (email, url, number…) |
| `novalidate` | Desliga a validação nativa no form inteiro |

```html
<!-- Campos com validação nativa -->
<input type="text"   name="nome"  required minlength="2" maxlength="60" />
<input type="email"  name="email" required />
<input type="number" name="idade" required min="18" max="120" />
<input type="url"    name="site" />

<!-- Pattern: apenas letras e números, 6 a 12 caracteres -->
<input
  type="text"
  name="usuario"
  pattern="[a-zA-Z0-9]{6,12}"
  title="Entre 6 e 12 letras ou números"
  required
/>

<!-- Desligar validação (útil ao salvar rascunho) -->
<form novalidate>...</form>
```

> **Dica:** `type="email"` já valida o formato — não precisa de `pattern` para e-mails simples. Use `pattern` para casos específicos como CPF, CEP ou códigos internos.

---

## Outros controles

| Tag / Atributo | Função |
|---|---|
| `<textarea>` | Área de texto grande — múltiplas linhas |
| `rows` | Altura inicial em linhas |
| `cols` | Largura em caracteres |
| `<select>` | Dropdown — lista de opções |
| `<option>` | Item do dropdown |
| `<optgroup>` | Agrupa opções com um rótulo |
| `<button type="submit">` | Envia o formulário |
| `<button type="button">` | Botão normal — não envia nada |
| `<button type="reset">` | Limpa todos os campos do form |
| `<datalist>` | Sugestões digitáveis — autocomplete aberto |

```html
<!-- Textarea -->
<label for="mensagem">Mensagem</label>
<textarea id="mensagem" name="mensagem" rows="5" cols="40" placeholder="Escreva aqui..."></textarea>

<!-- Select com optgroup -->
<label for="estado">Estado</label>
<select id="estado" name="estado">
  <optgroup label="Sudeste">
    <option value="SP">São Paulo</option>
    <option value="RJ">Rio de Janeiro</option>
  </optgroup>
  <optgroup label="Sul">
    <option value="PR">Paraná</option>
    <option value="RS">Rio Grande do Sul</option>
  </optgroup>
</select>

<!-- Botões -->
<button type="submit">Enviar</button>
<button type="button" onclick="abrirModal()">Abrir modal</button>
<button type="reset">Limpar</button>

<!-- Datalist: sugestões mas o usuário pode digitar outro valor -->
<label for="linguagem">Linguagem</label>
<input list="linguagens" id="linguagem" name="linguagem" />
<datalist id="linguagens">
  <option value="JavaScript" />
  <option value="Python" />
  <option value="TypeScript" />
</datalist>
```

---

## Tabelas

| Tag / Atributo | Função |
|---|---|
| `<table>` | Container da tabela |
| `<thead>` | Cabeçalho — agrupa as linhas de título |
| `<tbody>` | Dados — corpo principal da tabela |
| `<tfoot>` | Rodapé — totais, notas finais |
| `<tr>` | Linha — table row |
| `<th>` | Cabeçalho da célula — negrito e centralizado por padrão |
| `<td>` | Dado — célula comum |
| `scope` | Define a direção do cabeçalho: `col` ou `row` |
| `colspan` | Junta colunas horizontalmente |
| `rowspan` | Junta linhas verticalmente |
| `<caption>` | Título da tabela — lido por leitores de tela |

```html
<table>
  <caption>Comparativo de planos</caption>

  <thead>
    <tr>
      <th scope="col">Recurso</th>
      <th scope="col">Básico</th>
      <th scope="col">Pro</th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>Usuários</td>
      <td>1</td>
      <td>10</td>
    </tr>
    <tr>
      <td>Armazenamento</td>
      <td>5 GB</td>
      <td>100 GB</td>
    </tr>
    <tr>
      <td colspan="2">Disponível apenas no Pro</td>
      <td>API access</td>
    </tr>
  </tbody>

  <tfoot>
    <tr>
      <th scope="row">Preço/mês</th>
      <td>Grátis</td>
      <td>R$ 49</td>
    </tr>
  </tfoot>

</table>
```

> **Dica:** use `scope="col"` nos `<th>` do cabeçalho e `scope="row"` nos `<th>` laterais. Isso permite que leitores de tela anunciem corretamente qual dado pertence a qual cabeçalho — especialmente importante em tabelas grandes.
