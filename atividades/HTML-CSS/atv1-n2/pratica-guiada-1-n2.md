# Prática guiada: construção de uma barra de navegação para um blog técnico

Nesta atividade, você irá construir uma **barra de navegação (navbar)** semelhante à de um blog técnico moderno.

O foco da prática está em quatro pilares fundamentais:

* **estrutura semântica do HTML**;
* **separação entre HTML e CSS externo**;
* **uso de variáveis CSS (tokens de design)**;
* **construção de layout com Flexbox, passo a passo**.

> 📌 Nesta prática inicial, não iremos tratar de acessibilidade. O objetivo é consolidar os fundamentos e praticar um pouco de responsividade com uso de media queries (ao final da atividade).

---

## Objetivos de aprendizagem

Ao final da atividade, você deverá ser capaz de:

* estruturar corretamente uma navbar com HTML semântico;
* organizar estilos em um arquivo CSS externo;
* utilizar variáveis CSS para padronização visual;
* aplicar Flexbox para construir layouts horizontais;
* compreender o impacto de cada propriedade no resultado visual;
* testar e ajustar a interface para diferentes tamanhos de tela.

---

## Estrutura do projeto

Crie dois arquivos:

* `index.html`
* `styles.css`

---

# 1) Construindo a estrutura HTML

Crie o arquivo `index.html`:

```html id="html-navbar"
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="utf-8">
  <title>BlogTech — Navbar</title>

  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700;900&display=swap" rel="stylesheet">
  <link href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined" rel="stylesheet">

  <link rel="stylesheet" href="styles.css">
</head>

<body>

<header class="site-header">
  <nav class="nav-inner">

    <!-- Logo -->
    <a href="#" class="nav-logo">BlogTech</a>

    <!-- Links -->
    <ul class="nav-links">
      <li><a href="#">Início</a></li>
      <li><a href="#">Artigos</a></li>
      <li><a href="#">Sobre</a></li>
    </ul>

    <!-- Ações -->
    <div class="nav-actions">
      <a href="#" class="btn-entrar">Entrar</a>
      <button class="btn-search">
        <span class="material-symbols-outlined">search</span>
      </button>
    </div>

  </nav>
</header>

</body>
</html>
```

---

## Entendendo a estrutura

A navbar foi organizada em três blocos principais:

* **logo** → identificação do site;
* **links centrais** → navegação principal;
* **ações** → interações do usuário.

> 💡 **Por que usar HTML semântico?**
>
> Elementos como `<header>` e `<nav>` ajudam a estruturar melhor o documento, facilitando leitura, manutenção e organização do código.

---

# 2) Criando o CSS externo

Agora crie o arquivo `styles.css`.

A seguir, vamos construir o estilo **em etapas progressivas**, entendendo o efeito de cada bloco.

---

# Etapa 1 — Reset e base da página

```css id="css-etapa1"
*, *::before, *::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Inter', sans-serif;
  background: #0e0e0e;
  color: #ffffff;
  min-height: 100vh;
}
```

### O que está acontecendo aqui?

* removemos espaçamentos padrão do navegador;
* definimos a fonte principal;
* aplicamos cores base da interface.

> 💡 **Importante**
>
> Sem esse reset, diferentes navegadores aplicariam estilos próprios, gerando inconsistências.

---

# Etapa 2 — Variáveis CSS (tokens de design)

Agora vamos centralizar valores reutilizáveis:

```css id="css-etapa2"
:root {
  --color-bg: #0e0e0e;
  --color-surface: rgba(26, 25, 25, 0.80);
  --color-primary: #a3a6ff;
  --color-text: #ffffff;
  --color-text-muted: #adaaaa;

  --nav-height: 64px;
  --nav-padding: 2rem;
}
```

Atualize o `body`:

```css id="css-etapa2b"
body {
  font-family: 'Inter', sans-serif;
  background: var(--color-bg);
  color: var(--color-text);
}
```

### Por que isso é importante?

As variáveis permitem:

* padronização visual;
* manutenção mais simples;
* reutilização de valores.

> 🎯 **Exemplo prático**
>
> Alterar `--color-primary` muda automaticamente todos os elementos que usam essa cor.

---

# Etapa 3 — Estrutura inicial da navbar

```css id="css-etapa3"
.site-header {
  height: var(--nav-height);
  background: var(--color-surface);
}
```

### Resultado esperado

Uma faixa horizontal no topo da página.

> 🔍 Neste momento, ainda não há organização interna dos elementos.

---

# Etapa 4 — Ativando o Flexbox

```css id="css-etapa4"
.nav-inner {
  display: flex;
}
```

### O que mudou?

Todos os elementos internos agora ficam **lado a lado**.

> 💡 **Conceito-chave**
>
> O Flexbox organiza os elementos no eixo horizontal por padrão.

---

# Etapa 5 — Alinhamento vertical

```css id="css-etapa5"
.nav-inner {
  display: flex;
  align-items: center;
  height: 100%;
}
```

### Resultado

Os itens ficam centralizados verticalmente dentro da navbar.

---

# Etapa 6 — Distribuição horizontal

```css id="css-etapa6"
.nav-inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 100%;
  padding: 0 var(--nav-padding);
}
```

### Resultado visual

* logo → esquerda
* links → centro
* ações → direita

> 🔍 **Entendimento essencial**
>
> `justify-content: space-between` distribui os elementos ocupando todo o espaço disponível.

---

# Etapa 7 — Organizando os links com Flexbox

```css id="css-etapa7"
.nav-links {
  display: flex;
  gap: 2rem;
  list-style: none;
}
```

### O que isso resolve?

* remove os marcadores da lista;
* coloca os itens lado a lado;
* adiciona espaçamento entre eles.

---

# Etapa 8 — Estilizando o logo

```css id="css-etapa8"
.nav-logo {
  font-size: 1.25rem;
  font-weight: 900;
  text-decoration: none;
  color: var(--color-text);
}
```

---

# Etapa 9 — Estilizando os links

```css id="css-etapa9"
.nav-links a {
  text-decoration: none;
  color: var(--color-text-muted);
  font-weight: 500;
}

.nav-links a:hover {
  color: var(--color-text);
}
```

> 💡 **Observação**
>
> O estado `:hover` melhora a percepção visual de interação.

---

# Etapa 10 — Container das ações

```css id="css-etapa10"
.nav-actions {
  display: flex;
  gap: 1rem;
  align-items: center;
}
```

### Resultado

Os elementos da direita passam a ficar alinhados horizontalmente.

---

# Etapa 11 — Botão "Entrar"

```css id="css-etapa11"
.btn-entrar {
  text-decoration: none;
  color: var(--color-primary);
  border: 1px solid #484847;
  padding: 0.25rem 0.75rem;
  border-radius: 0.5rem;
  font-weight: 700;
}
```

---

# Etapa 12 — Botão de busca

```css id="css-etapa12"
.btn-search {
  background: none;
  border: none;
  color: var(--color-text-muted);
  font-size: 1.3rem;
  cursor: pointer;
}
```

---

# 3) Atividade prática

Após concluir a implementação:

1. Teste a interface em diferentes tamanhos de tela para observar a resposividade;
2. Aplique medias queries para ajustar o layout em telas menores;
3. Experimente alterar as variáveis CSS para ver como o design se adapta.

> 🧪 **Exploração**
>
> O aprendizado mais efetivo ocorre quando você testa e observa mudanças no layout.

---

# 4) Síntese final

Nesta prática, você construiu uma interface real aplicando conceitos fundamentais:

* HTML define a **estrutura**;
* CSS define a **aparência**;
* variáveis CSS garantem **consistência**;
* Flexbox organiza o **layout horizontal**.

> ✅ **Conclusão**
>
> A construção passo a passo permite compreender não apenas *o que fazer*, mas principalmente *por que cada decisão foi tomada*.