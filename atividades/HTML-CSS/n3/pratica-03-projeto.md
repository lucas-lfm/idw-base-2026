# Prática guiada: construção do conteúdo principal da página inicial

> **Continuação da Prática 02 — Hero e Rodapé**
>
> Nesta terceira prática, daremos continuidade ao projeto desenvolvido nas aulas anteriores. A barra de navegação, a seção Hero e o rodapé permanecerão exatamente como foram implementados na prática anterior. Agora, construiremos a **área principal da página inicial**, composta por uma **grade de artigos** e uma **barra lateral (sidebar)**, aproximando o projeto de um blog moderno.
>
> Além disso, conheceremos uma nova técnica de construção de layouts: o **CSS Grid Layout**, ideal para organizar conteúdos em duas dimensões.

- **Resultado Final Esperado:**

![](./img/pratica03_final.png)

---

# Objetivos de aprendizagem

Ao final desta atividade, você deverá ser capaz de:

- compreender quando utilizar **CSS Grid** em vez de Flexbox;
- construir layouts bidimensionais utilizando Grid Layout;
- estruturar uma grade de artigos reutilizando um mesmo componente HTML;
- criar componentes reutilizáveis (cards);
- organizar diferentes regiões de conteúdo utilizando múltiplos contêineres;
- aplicar boas práticas de separação entre conteúdo e apresentação;
- reutilizar as variáveis CSS e os padrões definidos nas práticas anteriores;
- construir uma barra lateral (sidebar) contendo diferentes componentes da interface;
- compreender o conceito de composição de interfaces a partir de componentes independentes.

---

# Continuidade da estrutura do projeto

Toda a estrutura construída nas práticas anteriores será mantida.

Nesta atividade será implementada apenas a região indicada pelo comentário existente no arquivo `index.html`.

```html
<!-- Seção de conteúdo principal: grade de artigos e barra lateral (Prática 03) -->
```

Não serão realizadas alterações na navbar, na Hero ou no rodapé.

---

# Estrutura do projeto

Será criado apenas um novo arquivo CSS.

```text
css/
├── style.css
├── hero.css
├── footer.css
└── main.css
```

Adicione o novo arquivo ao `<head>` do documento.

```html
<link rel="stylesheet" href="./css/main.css" />
```

---

# 1) Criando a estrutura principal

Dentro da tag `<main>`, logo abaixo da Hero, adicione uma nova seção para o conteúdo principal.

```html
<section class="main-content">
  <div class="content-container">
    <!-- Grade de artigos -->

    <!-- Barra lateral -->
  </div>
</section>
```

## Entendendo essa estrutura

Assim como fizemos na Hero, criaremos um **container central** que limitará a largura da página e organizará seus elementos internos.

Observe que essa estrutura será responsável por dividir a tela em duas regiões:

- conteúdo principal;
- barra lateral.

---

# 2) Criando o container principal

Crie o arquivo `main.css`.

Começaremos pela estrutura geral.

```css
.main-content {
  padding: 0 3rem 5rem;
}

.content-container {
  max-width: var(--max-width-content);
  margin: 0 auto;
}
```

## O que está acontecendo aqui?

Mais uma vez reutilizamos o padrão adotado nas práticas anteriores.

Toda a interface utiliza a mesma largura máxima, mantendo consistência visual entre Navbar, Hero, conteúdo principal e rodapé.

---

# 3) Introduzindo o CSS Grid

Até agora utilizamos apenas Flexbox.

Nesta prática conheceremos uma nova técnica de construção de layouts: **CSS Grid Layout**.

Enquanto o Flexbox organiza elementos em apenas um eixo (linha ou coluna), o Grid permite organizar elementos em **linhas e colunas simultaneamente**, sendo ideal para layouts mais complexos.

Atualize o container:

```css
.content-container {
  display: grid;
}
```

Neste momento ainda não haverá mudanças visuais significativas.

---

# 4) Criando as duas regiões da página

Agora vamos dividir a página em duas colunas.

```css
.content-container {
  display: grid;

  grid-template-columns: 2fr 1fr;

  gap: 2.5rem;
}
```

## O que significa `2fr 1fr`?

A unidade **fr** representa uma fração do espaço disponível.

Neste caso:

- a área dos artigos ocupará aproximadamente dois terços da largura;
- a barra lateral ocupará aproximadamente um terço.

Essa abordagem torna o layout flexível e fácil de ajustar.

---

# 5) Criando a grade de artigos

Adicione a estrutura responsável pelos artigos.

```html
<section class="posts-grid">
  <!-- Card -->

  <!-- Card -->

  <!-- Card -->

  <!-- Card -->
</section>
```

Em seguida, aplique Grid novamente.

```css
.posts-grid {
  display: grid;

  grid-template-columns: repeat(2, 1fr);

  gap: 2rem;
}
```

Observe que agora temos um **Grid dentro de outro Grid**.

---

# 6) Construindo o primeiro Card

Todos os artigos seguirão exatamente a mesma estrutura.

Crie apenas um card inicialmente.

```html
<article class="post-card">
  <img />

  <div class="post-content">
    <span class="post-date"></span>

    <h2></h2>

    <p></p>

    <a href="#"></a>
  </div>
</article>
```

## Por que criar apenas um?

Porque esse componente será reutilizado diversas vezes.

Essa é uma prática muito comum no desenvolvimento moderno de interfaces.

---

# 7) Estilizando o Card

Começaremos pela estrutura externa.

```css
.post-card {
  background: var(--color-surface);

  border-radius: var(--border-radius);

  overflow: hidden;
}
```

## O que essas propriedades fazem?

- cria um fundo próprio para o card;
- arredonda os cantos;
- impede que a imagem ultrapasse os limites do cartão.

---

# 8) Organizando o conteúdo interno

Agora estilize a área textual.

```css
.post-content {
  padding: 1.5rem;
}
```

Posteriormente serão adicionados os estilos individuais para:

- data;
- título;
- descrição;
- botão "Ler mais".

Observe como o componente começa a ganhar identidade visual.

---

# 9) Reutilizando o componente

Depois de concluir o primeiro card, basta duplicá-lo.

Todos os artigos utilizarão exatamente a mesma estrutura HTML.

Essa reutilização reduz a quantidade de código e facilita futuras manutenções.

---

# 10) Criando a Sidebar

Ao lado da grade de artigos será criada uma barra lateral.

```html
<aside class="sidebar"></aside>
```

## Por que utilizar `<aside>`?

O elemento `<aside>` representa conteúdos complementares ao conteúdo principal da página.

Neste projeto, ele será utilizado para:

- newsletter;
- categorias;
- informações do autor.

---

# 11) Criando o componente Newsletter

O primeiro componente da Sidebar será um formulário simples.

Ele será composto por:

- título;
- texto;
- campo de e-mail;
- botão.

Além de ampliar a interface, esse componente introduz novos elementos HTML relacionados a formulários.

---

# 12) Criando a lista de categorias

Em seguida construiremos uma lista de categorias.

Cada linha será composta por:

- nome da categoria;
- quantidade de artigos.

Para alinhar essas informações utilizaremos novamente Flexbox.

```css
.category-item {
  display: flex;

  justify-content: space-between;

  align-items: center;
}
```

Observe que Grid e Flexbox podem ser utilizados juntos no mesmo projeto.

Cada um resolve um tipo diferente de problema.

---

# 13) Criando o Card do Autor

O último componente da Sidebar apresentará informações sobre o autor do blog.

Sua estrutura conterá:

- fotografia;
- nome;
- cargo;
- breve descrição.

Assim como os cards dos artigos, esse componente também poderá ser reutilizado em outras páginas.

---

# 14) Resultado esperado

Ao concluir esta prática, a página deverá apresentar:

- navbar construída na Prática 01;
- Hero construída na Prática 02;
- grade de artigos organizada com CSS Grid;
- sidebar contendo newsletter, categorias e card do autor;
- rodapé desenvolvido anteriormente.

![](./img/pratica03_final.png)

---

# Síntese final

Nesta prática você concluiu a estrutura principal da página inicial do BlogTech.

Os principais conceitos trabalhados foram:

- CSS Grid Layout;
- diferenças entre Grid e Flexbox;
- componentes reutilizáveis;
- construção de cards;
- composição de layouts complexos;
- utilização do elemento `<aside>`;
- organização da interface em múltiplas regiões;
- reutilização dos padrões visuais criados nas práticas anteriores.

> ✅ Nas próximas práticas, esses componentes poderão ser integrados ao JavaScript e posteriormente consumidos a partir de dados dinâmicos, aproximando o projeto de uma aplicação web real.
