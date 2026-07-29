# Prática guiada: construção da seção hero e rodapé

> **Continuação da Prática 01 — Barra de navegação**
>
> Nesta segunda prática, daremos continuidade ao projeto desenvolvido anteriormente. A barra de navegação construída na Prática 01 será mantida exatamente como está e servirá de base para a implementação da seção **Hero** e do **rodapé** do BlogTech.
>
> Além disso, iniciaremos uma organização mais modular dos estilos CSS, separando os arquivos por responsabilidade.

- **Resultado Final Esperado:**

![](./img/pratica02_final.png)

---

## Objetivos de aprendizagem

Ao final desta atividade, você deverá ser capaz de:

- estruturar uma seção Hero utilizando HTML semântico;
- utilizar Flexbox para distribuir elementos em diferentes regiões da página;
- compreender a utilização de contêineres para limitar a largura do conteúdo;
- organizar o CSS em arquivos modulares;
- reutilizar variáveis CSS criadas anteriormente;
- construir um rodapé moderno mantendo consistência visual com a navbar.

---

## Continuidade da estrutura do projeto

A estrutura criada na prática anterior será mantida.

Apenas serão adicionados dois novos arquivos CSS:

```text
css/
├── style.css      (já existente)
├── hero.css       (novo)
└── footer.css     (novo)
```

Também atualize o `<head>` do arquivo `index.html` para incluir os novos arquivos:

```html
<link rel="stylesheet" href="./css/style.css" />
<link rel="stylesheet" href="./css/hero.css" />
<link rel="stylesheet" href="./css/footer.css" />
```

---

# 1) Atualizando o arquivo index.html

Mantenha toda a navbar construída anteriormente.

Dentro da tag `<main>`, adicione a seção Hero:

```html
<main>
  <section class="hero-section" id="inicio">
    <div class="hero-container">
      <div class="hero-titulo-wrapper">
        <h1 class="hero-titulo">Bem-vindo ao Nosso Blog</h1>
      </div>

      <div class="hero-stats">
        <div class="stat-item">
          <span class="stat-valor">500 Comentários</span>
          <span class="stat-descricao">Interação ativa</span>
        </div>

        <div class="stat-item">
          <span class="stat-valor">10k Visualizações</span>
          <span class="stat-descricao">Alcance global</span>
        </div>
      </div>
    </div>
  </section>

  <!-- Seção de conteúdo principal: grade de artigos e barra lateral (Prática 03) -->
</main>
```

Após a tag `</main>`, adicione o rodapé:

```html
<footer class="site-footer">
  <div class="footer-container">
    <a href="./index.html" class="footer-brand"> BlogTech </a>

    <nav class="footer-nav">
      <a href="#">Privacidade</a>
      <a href="#">Termos</a>
      <a href="#">Contato</a>
    </nav>

    <p class="footer-copy">© 2026 BlogTech. Todos os direitos reservados.</p>
  </div>
</footer>
```

---

# 2) Atualizando o style.css

Acrescente ao bloco `:root` as novas variáveis:

```css
--base-font: "Inter", sans-serif;
--max-width-nav: 1400px;
--max-width-content: 1280px;
--border-radius: 0.5rem;

--color-border: rgba(72, 72, 71, 0.3);
--color-divisor: rgba(72, 72, 71, 0.15);
```

Atualize também a classe `.nav-inner`:

```css
.nav-inner {
  width: var(--max-width-nav);
  margin: 0 auto;
}
```

Essas variáveis serão reutilizadas pelas próximas seções, mantendo o projeto consistente.

---

# 3) Criando o arquivo hero.css

## Etapa 1 — Espaçamento da seção

```css
.hero-section {
  padding: 5rem 3rem 4rem;
}
```

A Hero recebe um espaçamento confortável em relação à navbar e ao restante da página.

---

## Etapa 2 — Container central

```css
.hero-container {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: flex-end;
  gap: 2rem;

  max-width: var(--max-width-content);
  margin: 0 auto;
}
```

Assim como na navbar, utilizamos um contêiner para limitar a largura do conteúdo e centralizá-lo.

---

## Etapa 3 — Área do título

```css
.hero-titulo-wrapper {
  flex: 1;
}

.hero-titulo {
  font-size: 6rem;
  font-weight: 900;
  line-height: 1.05;
  letter-spacing: -0.04em;
  color: var(--color-text);
}
```

Observe como o `flex:1` faz o título ocupar o espaço disponível, enquanto a área das estatísticas permanece alinhada à direita.

---

## Etapa 4 — Estatísticas

```css
.hero-stats {
  display: flex;
  flex-direction: row;
  gap: 2rem;
  padding-bottom: 1rem;
  flex-shrink: 0;
}

.stat-item {
  display: flex;
  flex-direction: column;
}

.stat-valor {
  font-size: 0.7rem;
  font-weight: 700;
  color: var(--color-primary);
  letter-spacing: 0.2em;
  text-transform: uppercase;
}

.stat-descricao {
  font-size: 0.875rem;
  margin-top: 0.25rem;
}
```

Cada estatística é organizada verticalmente utilizando Flexbox.

---

# 4) Criando o arquivo footer.css

## Etapa 1 — Estrutura do rodapé

```css
.site-footer {
  padding: 3rem;
  border-top: 1px solid var(--color-divisor);
}
```

A linha superior cria uma separação visual entre o conteúdo principal e o rodapé.

---

## Etapa 2 — Container

```css
.footer-container {
  display: flex;
  justify-content: space-between;
  align-items: center;

  max-width: var(--max-width-content);
  margin: 0 auto;
}
```

A estrutura segue o mesmo padrão utilizado na Hero.

---

## Etapa 3 — Marca

```css
.footer-brand {
  font-size: 1.25rem;
  font-weight: 700;
  color: var(--color-text);
  text-decoration: none;
  letter-spacing: -0.05em;
}
```

---

## Etapa 4 — Links institucionais

```css
.footer-nav {
  display: flex;
  gap: 2rem;
  flex-wrap: wrap;
}

.footer-nav a {
  color: var(--color-text-muted);
  text-decoration: none;
  font-size: 0.875rem;
  font-weight: 500;
}

.footer-nav a:hover {
  color: var(--color-primary);
}
```

---

## Etapa 5 — Direitos autorais

```css
.footer-copy {
  font-size: 0.875rem;
  color: var(--color-text-muted);
  font-weight: 500;
  opacity: 0.8;
}
```

---

# 5) Resultado esperado

Ao concluir esta prática, a página deverá apresentar:

- navbar construída na prática anterior;
- seção Hero semelhante ao layout apresentado;
- rodapé alinhado com o restante da interface;
- organização do CSS em módulos (`style.css`, `hero.css` e `footer.css`).

![](./img/pratica02_final.png)

---

# 6) Síntese final

Nesta prática você deu continuidade ao projeto iniciado anteriormente sem alterar sua estrutura principal.

Os principais conceitos trabalhados foram:

- modularização de arquivos CSS;
- reutilização de variáveis CSS;
- criação de layouts com Flexbox;
- utilização de contêineres para limitar largura;
- construção de uma Hero moderna;
- implementação de um rodapé consistente com o restante da interface.

> ✅ A próxima prática dará continuidade ao projeto implementando a área principal de conteúdo, composta pela grade de artigos e pela barra lateral.

---

## Lista de Exercícios

**Parte I – Questões objetivas**

1. Qual é a principal finalidade de utilizar um elemento `<main>` em uma página HTML?

a) Definir o menu principal do site.

b) Agrupar o conteúdo principal da página.

c) Inserir arquivos CSS externos.

d) Criar uma nova janela do navegador.

2. Na estrutura da Hero desenvolvida na prática, qual elemento contém o título principal da página?

a) `.hero-container`

b) `.hero-stats`

c) `.hero-titulo`

d) `.hero-section`

3. Qual propriedade do Flexbox foi utilizada para posicionar o título à esquerda e as estatísticas à direita?

a) `align-items`

b) `gap`

c) `justify-content: space-between`

d) `flex-wrap`

4. Qual é a principal vantagem de utilizar um contêiner com largura máxima (`max-width`) e `margin: 0 auto`?

a) Fazer o conteúdo ocupar toda a largura da tela.

b) Centralizar o conteúdo e evitar que fique excessivamente largo em telas grandes.

c) Tornar a página responsiva automaticamente.

d) Aumentar o tamanho das fontes.

5. Na prática, os estilos da Hero foram colocados em um arquivo separado (hero.css). Qual o principal benefício dessa organização?

a) O navegador passa a carregar o CSS mais rapidamente.

b) O HTML fica menor.

c) O código fica mais organizado e facilita a manutenção.

d) O CSS passa a funcionar apenas nessa página.

6. No rodapé, qual elemento HTML foi utilizado para agrupar os links institucionais?

a) `<section>`

b) `<header>`

c) `<nav>`

d) `<aside>`

7. A variável `--max-width-content` foi criada com qual objetivo?

a) Definir a altura máxima da página.

b) Limitar a largura das seções de conteúdo e manter o alinhamento visual.

c) Definir o tamanho máximo das imagens.

d) Controlar a largura da barra de rolagem.

8. Observe o trecho abaixo:

```css
.hero-titulo-wrapper {
  flex: 1;
}
```

O efeito dessa propriedade é:

a) impedir que o elemento seja exibido.

b) fazer o elemento ocupar o espaço disponível dentro do Flexbox.

c) centralizar o texto horizontalmente.

d) aumentar automaticamente o tamanho da fonte.

**Parte II – Questões discursivas**

9. Explique por que a modularização do CSS (separando style.css, hero.css e footer.css) é considerada uma boa prática em projetos de desenvolvimento web.

10. Na Hero construída durante a prática, foi utilizado um contêiner (hero-container) envolvendo o título e as estatísticas. Explique qual é a função desse contêiner no layout.

11. Imagine que o projeto continuará crescendo e passará a possuir diversas seções (artigos, sidebar, newsletter, comentários etc.). Que vantagens essa organização modular do HTML e do CSS oferece para a manutenção do projeto? Cite pelo menos três vantagens.

12. Durante a prática foram utilizadas diversas variáveis CSS, como:

```css
--color-primary
--color-text
--max-width-content
```

Explique o que são variáveis CSS e descreva duas vantagens de utilizá-las em um projeto.

**Parte III – Desafio**

13. Observe a seguinte estrutura:

```html
<div class="hero-stats">
  <div class="stat-item">
    <span class="stat-valor">500 Comentários</span>
    <span class="stat-descricao">Interação ativa</span>
  </div>
</div>
```

Suponha que você precise adicionar uma terceira estatística chamada "120 Artigos Publicados", mantendo o mesmo padrão visual da página. Como você faria isso? Escreva o código HTML necessário para adicionar essa nova estatística. É necessário adicionar ou alterar algum CSS? Justifique sua resposta.

**Parte IV – Reflexão**

14. Durante a construção da navbar, da Hero e do rodapé, qual conceito foi mais fácil de compreender e qual apresentou maior dificuldade? Justifique sua resposta.
