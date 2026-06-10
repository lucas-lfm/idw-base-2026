# Introdução ao Desenvolvimento Web - Redes 3

## **_Projeto BlogTech: prática guiada 02_** - (Parte 02) Seção Hero e Rodapé

> - **Objetivo:** dar continuidade ao projeto BlogTech construindo a seção de destaque (_hero_) e o rodapé (_footer_) da página inicial, utilizando HTML semântico, Flexbox e tokens de design já definidos na prática anterior, além de novos conceitos apresentados ao longo deste roteiro.
> - **Observações e Instruções Gerais:**
>   - Esta prática é a continuação direta da **[Prática Guiada 01](./../atv1-n2/)**. Certifique-se de que o projeto está com a estrutura e os arquivos da prática anterior antes de começar.
>   - Tente seguir o roteiro de forma a entender cada passo.
>   - Caso fique com alguma dúvida, fique à vontade para perguntar.

---

### 1. Apresentação da Prática

- Esta prática dá continuidade ao projeto **BlogTech**. Partindo da barra de navegação já construída na Prática Guiada 01, vamos agora implementar a **seção hero** — a área de destaque que o usuário vê ao acessar a página — e o **rodapé** do site.

- A seção hero que vamos construir é composta por:
  - Um **título de impacto** à esquerda ("Bem-vindo ao Nosso Blog")
  - Dois **indicadores de estatísticas** alinhados ao rodapé do lado direito (comentários e visualizações)

- O rodapé terá:
  - O **logotipo** textual do blog à esquerda
  - **Links institucionais** centralizados (Privacidade, Termos, Contato)
  - **Texto de direitos autorais** à direita

<!-- - O resultado esperado ao final desta prática é o seguinte:

  ![Resultado esperado: seção hero com título em destaque à esquerda e estatísticas à direita, seguida do rodapé com logotipo, links e copyright](img-instrucoes/screen-hero-footer.png) -->

- O que vamos aplicar nesta prática?
  - Atualização dos tokens de design (novas variáveis CSS no `:root`)
  - Elemento semântico `<section>` para a seção hero e `<footer>` para o rodapé
  - **Flexbox** com `align-items: flex-end` para alinhamento vertical na base do container
  - Propriedade `flex-shrink` para controlar o comportamento dos elementos flexíveis
  - Tipografia de grande escala para títulos de impacto
  - `text-transform` e `letter-spacing` para estilização de rótulos
  - Separação de estilos por componente (`hero.css` e `footer.css`)
  - Preparação de espaço para a seção de conteúdo principal (próxima prática)

---

### 2. Atualizando os tokens de design

> Antes de escrever qualquer HTML ou CSS novo, vamos adicionar ao nosso arquivo de estilos globais os tokens de design necessários para esta etapa. Lembre-se: centralizar valores em variáveis garante consistência e facilita futuras alterações.

1. Abra o arquivo `css/style.css` e localize o bloco `:root` definido na prática anterior.

1. Adicione as novas variáveis abaixo, nos respectivos grupos de comentário:

   ```css
   :root {
     --color-bg: #0e0e0e;
     --color-surface: rgba(26, 25, 25, 0.8);
     --color-primary: #a3a6ff;
     --color-text: #ffffff;
     --color-text-muted: #adaaaa;

     --nav-height: 64px;
     --nav-padding: 2rem;

     /* Prática 02 */
     --color-text-secondary: #c1c1c1; /* ← NOVO: cor de texto secundária para descrições e detalhes */
     --base-font:
       "Inter", sans-serif; /* ← NOVO: define a fonte base para todas as seções */
     --max-width-nav: 1400px; /* ← NOVO: largura máxima da barra de navegação */
     --max-width-content: 1280px; /* ← NOVO: largura máxima das seções de conteúdo */
     --border-radius: 0.5rem; /* ← NOVO: borda arredondada para botões e elementos de destaque */
     --color-border: rgba(
       72,
       72,
       71,
       0.3
     ); /* ← NOVO: cor de borda suave para elementos como botões e cards */
     --color-divisor: rgba(
       72,
       72,
       71,
       0.15
     ); /* ← NOVO: cor de divisor ainda mais suave para linhas de separação */
   }
   ```

   - **`--color-divisor`**: uma cor de borda ainda mais suave do que `--color-border` (0.15 de opacidade vs 0.3). Ela será usada para a linha horizontal que separa o rodapé do conteúdo acima. Uma separação muito marcada quebraria a fluidez visual do design escuro.

   - **`--max-width-content`**: enquanto `--max-width-nav` (1400px) define a largura da barra de navegação, as seções de conteúdo precisam de uma largura máxima um pouco menor (1280px) para ficarem mais concentradas e legíveis, especialmente quando o texto é muito grande, como o título da hero.

   > 💡 Perceba que esses dois valores são diferentes intencionalmente. A navbar ocupa toda a barra horizontal da tela e "sangra" até as bordas — por isso pode ser um pouco mais larga. Já as seções de conteúdo precisam de margens mais generosas para respirar. Essa distinção é uma decisão de design que afeta diretamente a experiência do usuário.
   - **`--base-font`**: definimos a fonte base para todo o projeto. Embora tenhamos importado a fonte Inter no `index.html`, esta variável nos permite referenciá-la facilmente em qualquer arquivo CSS, garantindo que todos os componentes usem a mesma família tipográfica sem precisar repetir a declaração de importação.

   - **`--border-radius`**: um valor de borda arredondada que usaremos para botões e elementos de destaque, como os cards de artigos que implementaremos na próxima prática. O uso de bordas arredondadas é uma escolha estética que suaviza o design e cria uma sensação mais moderna e amigável.

1. Ainda no arquivo `style.css`, vamos definir a largura máxima e centralização da barra de navegação, seguindo o mesmo padrão que usaremos para as seções de conteúdo:

   ```css
   .nav-inner {
     display: flex;
     align-items: center;
     justify-content: space-between;
     height: 100%;
     padding: 0 var(--nav-padding);
     max-width: var(
       --max-width-nav
     ); /* ← NOVO: largura máxima da barra de navegação */
     margin: 0 auto; /* ← NOVO: centraliza a barra de navegação horizontalmente */
   }
   ```

1. Para finaizar, adiocione no arquivo `style.css` uma regra geral para o elemento `main`, definindo a largura máxima e centralização, assim como um `margin-top` para criar espaço abaixo da navbar fixa:

   ```css
   main {
     max-width: var(
       --max-width-content
     ); /* ← NOVO: largura máxima das seções de conteúdo */
     margin: 2rem auto 0; /* ← NOVO: centraliza o conteúdo e adiciona margem superior para espaçamento abaixo da navbar */
     padding: 0 1rem; /* ← NOVO: padding horizontal para garantir que o conteúdo não encoste nas bordas em telas pequenas */
   }
   ```

   > Você pode inserir a regra do `main` logo após a definição do `body` no `style.css`, para manter a organização dos estilos globais.

---

### 3. Atualizando o HTML

> Vamos atualizar o `index.html` para adicionar a seção hero dentro do `<main>` e o rodapé logo após. Além disso, vamos referenciar os dois novos arquivos CSS que criaremos nas próximas seções.

1. Abra o arquivo `index.html`.

1. Na seção `<head>`, adicione as referências aos dois novos arquivos CSS que criaremos em seguida. Inclua as linhas abaixo **após** a referência ao `style.css`:

   ```html
   <link rel="stylesheet" href="./css/hero.css" />
   <link rel="stylesheet" href="./css/footer.css" />
   ```

   - A seção `<head>` de links ficará assim:
     ```html
     <link rel="stylesheet" href="./css/style.css" />
     <link rel="stylesheet" href="./css/hero.css" />
     <link rel="stylesheet" href="./css/footer.css" />
     ```

1. Agora, **crie o elemento `<main>`**, logo após o elemento `header`, inserindo a seção hero e um comentário reservando o espaço para a próxima prática:

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

   - Entendendo a estrutura da seção hero:
     - **`<section class="hero-section" id="inicio">`**: usamos `<section>` por ser um bloco de conteúdo temático com significado próprio. O `id="inicio"` conecta esta seção ao link _Início_ da navbar (que aponta para `#inicio`), permitindo a navegação por âncora na página.
     - **`.hero-container`**: o contêiner interno que usaremos com Flexbox para posicionar o título e os indicadores lado a lado. Seguindo o mesmo padrão do `.nav-inner` da prática anterior.
     - **`.hero-titulo-wrapper`**: uma `<div>` que envolve o título, permitindo controlar como ele cresce e ocupa o espaço disponível dentro do Flexbox.
     - **`<h1 class="hero-titulo">`**: usamos `<h1>` pois este é o título principal da página — deve existir apenas um `<h1>` por página, e ele representa o tema central do conteúdo.
     - **`.hero-stats`**: agrupa os dois indicadores de estatísticas. Cada `.stat-item` contém um `.stat-valor` (o número em destaque) e um `.stat-descricao` (o texto explicativo abaixo).
     - O **comentário** ao final do `<main>` reserva o espaço para a grade de artigos e a barra lateral, que serão implementados na próxima prática.

1. Ainda no `index.html`, **após o fechamento de `</main>`**, adicione o elemento `<footer>`:

   ```html
   <footer class="site-footer">
     <div class="footer-container">
       <a href="./index.html" class="footer-brand">BlogTech</a>

       <nav class="footer-nav" aria-label="Links institucionais">
         <a href="#">Privacidade</a>
         <a href="#">Termos</a>
         <a href="#">Contato</a>
       </nav>

       <p class="footer-copy">© 2026 BlogTech. Todos os direitos reservados.</p>
     </div>
   </footer>
   ```

   - Entendendo a estrutura do rodapé:
     - **`<footer class="site-footer">`**: o elemento `<footer>` é semanticamente correto para rodapés de página. Ele fica fora do `<main>` porque não é conteúdo principal — é informação institucional e de navegação secundária.
     - **`.footer-container`**: segue o mesmo padrão dos outros contêineres do projeto (max-width + margin auto), garantindo que o conteúdo fique centrado e alinhado com as demais seções.
     - **`<a class="footer-brand">`**: o logotipo no rodapé, como link para o topo da página, é uma convenção amplamente adotada na web.
     - **`<nav class="footer-nav" aria-label="Links institucionais">`**: usamos `<nav>` aqui também, pois é um grupo de links de navegação. O `aria-label` diferencia este `<nav>` do `.nav-inner` do cabeçalho para leitores de tela.
     - **`<p class="footer-copy">`**: o texto de copyright é um parágrafo simples — sem necessidade de hierarquia semântica adicional.

1. O código completo e atualizado do `index.html` deve ficar assim:

   ```html
   <!doctype html>
   <html lang="pt-BR">
     <head>
       <meta charset="utf-8" />
       <meta name="viewport" content="width=device-width, initial-scale=1.0" />
       <title>BlogTech — Navbar</title>

       <link
         href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700;900&display=swap"
         rel="stylesheet"
       />
       <link
         href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined"
         rel="stylesheet"
       />

       <link rel="stylesheet" href="./css/style.css" />
       <link rel="stylesheet" href="./css/hero.css" />
       <link rel="stylesheet" href="./css/footer.css" />
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

            <button class="btn-hamburger">
              <span class="material-symbols-outlined">menu</span>
            </button>
          </nav>
        </header>

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

        <footer class="site-footer">
          <div class="footer-container">
            <a href="./index.html" class="footer-brand">BlogTech</a>

            <nav class="footer-nav" aria-label="Links institucionais">
              <a href="#">Privacidade</a>
              <a href="#">Termos</a>
              <a href="#">Contato</a>
            </nav>

            <p class="footer-copy">
              © 2026 BlogTech. Todos os direitos reservados.
            </p>
          </div>
        </footer>

        <script>
          let menu = document.querySelector(".btn-hamburger");
          let nav = document.querySelector(".nav-inner");

          menu.addEventListener("click", () => {
            nav.classList.toggle("open");
          });
        </script>

      </body>
    </html>
    ```

- A estrutura do projeto na pasta `css/` ficará com mais dois arquivos:

  ```
  blogtech/
  ├── css/
  │   ├── style.css
  │   ├── hero.css    ← novo
  │   └── footer.css  ← novo
  └── index.html
  ```

---

### 4. CSS para a seção hero

> Agora vamos construir o arquivo `hero.css`. O ponto central desta seção é entender como o Flexbox se comporta com `align-items: flex-end` — o que nos permite alinhar elementos de alturas diferentes pela sua borda inferior, criando o efeito visual onde as estatísticas ficam "ancoradas" na base do título.

1. Crie o arquivo `css/hero.css`.

2. Vamos começar estilizando o elemento `<section>` pela classe `.hero-section`. Ele precisa de espaçamento interno generoso para que o título respire e o impacto visual seja alcançado:

```css
.hero-section {
  padding: 5rem 3rem 4rem;
}
```

- `padding: 5rem 3rem 4rem` define: **5rem** no topo (para separar da navbar e criar altura visual), **3rem** nas laterais (espaçamento horizontal interno) e **4rem** na base.
- Perceba que o `<main>` já tem `margin-top: var(--altura-nav)` definido na prática anterior, empurrando o conteúdo para baixo da navbar fixa. O `padding-top` da seção hero adiciona ainda mais espaço acima do título, dando o "ar" que grandes títulos precisam.

3. Agora vamos criar o `.hero-container`, o contêiner interno com Flexbox:

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

   - **`align-items: flex-end`**: este é o detalhe mais importante do layout da hero! Ao contrário do `align-items: center` que usamos na navbar, aqui queremos que o título e as estatísticas fiquem alinhados pela **borda inferior** do container. O título é muito mais alto do que os estatísticas — com `flex-end`, as estatísticas ficam "ancoradas" na base, ao lado da linha final do título. Veja a diferença:

     | `align-items` | Comportamento                                             |
     | ------------- | --------------------------------------------------------- |
     | `flex-start`  | os dois grupos ficam alinhados pelo topo                  |
     | `center`      | os dois grupos ficam alinhados pelo centro                |
     | `flex-end`    | os dois grupos ficam alinhados pela base ← **nosso caso** |

   - **`justify-content: space-between`**: empurra o título para a esquerda e as estatísticas para a direita, aproveitando toda a largura disponível.
   - **`max-width: var(--max-width-content)`** com **`margin: 0 auto`**: limita a largura e centraliza o conteúdo, exatamente como fizemos com `.nav-inner` e `.footer-container`.

4. Vamos estilizar o `.hero-titulo-wrapper`. Ele precisa crescer para ocupar o espaço disponível ao lado das estatísticas:

   ```css
   .hero-titulo-wrapper {
     flex: 1;
   }
   ```

   - A propriedade `flex: 1` é uma abreviação de `flex-grow: 1; flex-shrink: 1; flex-basis: 0`. Na prática, ela faz com que o wrapper do título **cresça** para preencher todo o espaço horizontal que sobrar depois que as estatísticas ocuparem o espaço delas. O resultado é que o título sempre terá a maior área possível — e o texto vai quebrar de linha naturalmente quando a largura for atingida.

5. O elemento central desta seção é o `<h1>`. Vamos dar a ele o tamanho e a personalidade visual que o design exige:

   ```css
   .hero-titulo {
     font-size: 6rem;
     font-weight: 900;
     line-height: 1.05;
     letter-spacing: -0.04em;
     color: var(--color-text);
   }
   ```

   - **`font-size: 6rem`**: 6 vezes o tamanho padrão da fonte (~96px). Títulos de impacto em blogs e landing pages frequentemente usam tamanhos assim para criar hierarquia visual imediata.
   - **`font-weight: 900`**: o peso máximo da fonte Inter — o mesmo usado no logotipo "BlogTech" na navbar, reforçando a identidade visual.
   - **`line-height: 1.05`**: espaçamento entre linhas levemente acima de 1 (que seria sem espaço extra). Como o título vai quebrar em duas linhas ("Bem-vindo ao / Nosso Blog"), esse valor garante que as linhas fiquem bem próximas — uma escolha tipográfica comum em títulos grandes, que transmite coesão e força.
   - **`letter-spacing: -0.04em`**: reduz o espaço entre letras em 4% do tamanho da fonte. Em tamanhos grandes, as letras ficam visualmente "afastadas" demais, e um `letter-spacing` negativo corrige isso, deixando o bloco de texto mais denso e impactante. Saiba mais sobre tipografia para web [neste link](https://web.dev/articles/font-best-practices).

6. Agora vamos organizar o container das estatísticas:

   ```css
   .hero-stats {
     display: flex;
     flex-direction: row;
     gap: 2rem;
     padding-bottom: 1rem;
     flex-shrink: 0;
   }
   ```

   - **`flex-direction: row`**: coloca os dois indicadores lado a lado.
   - **`padding-bottom: 1rem`**: empurra levemente os indicadores para cima da borda inferior do container. Sem isso, eles ficariam exatamente na base, sem respiro.
   - **`flex-shrink: 0`**: esta propriedade impede que as estatísticas **encolham** quando o espaço horizontal for reduzido. Por padrão, itens flex podem diminuir de tamanho quando o container é pequeno. Com `flex-shrink: 0`, garantimos que as estatísticas mantenham sempre o seu tamanho natural — e se precisar ceder espaço, será o `.hero-titulo-wrapper` (que tem `flex: 1`) a fazer isso. Saiba mais sobre o modelo flex [neste link](https://developer.mozilla.org/pt-BR/docs/Web/CSS/flex-shrink).

7. Cada `.stat-item` organiza verticalmente o valor e a descrição:

   ```css
   .stat-item {
     display: flex;
     flex-direction: column;
   }
   ```

   - Nada de novo aqui — Flexbox com `flex-direction: column` para empilhar os dois `<span>` verticalmente dentro de cada indicador.

8. Por fim, vamos estilizar os textos dos indicadores:

   ```css
   .stat-valor {
     font-size: 0.7rem;
     font-weight: 700;
     color: var(--color-primary);
     letter-spacing: 0.2em;
     text-transform: uppercase;
   }

   .stat-descricao {
     font-size: 0.875rem;
     color: var(--color-text-secondary);
     margin-top: 0.25rem;
   }
   ```

   - **`text-transform: uppercase`**: transforma o texto em maiúsculas via CSS, sem precisar escrever "500 COMENTÁRIOS" no HTML. Isso é uma boa prática: o HTML registra o conteúdo semântico (o que o texto diz), e o CSS define a apresentação (como ele aparece).
   - **`letter-spacing: 0.2em`**: em textos muito pequenos em caixa alta (_all caps_), um espaçamento generoso entre letras melhora muito a legibilidade e dá um ar mais sofisticado. Compare `DESIGN` vs `D E S I G N` — o segundo "respira" mais.
   - **`color: var(--color-primary)`**: usamos o azul-lavanda primário para dar destaque aos números, tornando-os o ponto focal dos indicadores.

8. O código final do `hero.css` deve ficar assim:

   ```css
   .hero-section {
     padding: 5rem 3rem 4rem;
   }

   .hero-container {
     display: flex;
     flex-direction: row;
     justify-content: space-between;
     align-items: flex-end;
     gap: 2rem;
     max-width: var(--max-width-content);
     margin: 0 auto;
   }

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
     color: var(--color-text-secondary);
     margin-top: 0.25rem;
   }
   ```

---

### 5. CSS para o rodapé

> O rodapé segue os mesmos padrões de layout já praticados — Flexbox com `justify-content: space-between` para distribuir três grupos horizontalmente. A diferença está na separação visual pelo `border-top` e na paleta de cores mais discreta, condizente com o papel secundário de um rodapé.

1. Crie o arquivo `css/footer.css`.

1. Vamos estilizar o elemento `<footer>` pela classe `.site-footer`:

   ```css
   .site-footer {
     padding: 3rem;
     border-top: 1px solid var(--color-divisor);
   }
   ```

   - **`border-top`**: uma linha horizontal muito sutil (opacidade de 15%) que separa o rodapé do conteúdo acima. Usando a variável `--color-divisor` que acabamos de definir. Uma linha muito marcada seria pesada demais num design escuro — a sutileza é intencional.
   - **`padding: 3rem`**: espaçamento interno generoso, dando ao rodapé o mesmo "ar" das outras seções.

1. Agora o `.footer-container`, que centraliza e limita o conteúdo. O padrão já é familiar:

   ```css
   .footer-container {
     display: flex;
     flex-direction: row;
     justify-content: space-between;
     align-items: center;
     max-width: var(--max-width-content);
     margin: 0 auto;
   }
   ```

   - `align-items: center` alinha os três grupos (brand, nav, copyright) verticalmente ao centro — diferente da hero, onde usamos `flex-end`. No rodapé, todos os elementos têm alturas similares, então o centro faz mais sentido visualmente.
   - Perceba que este é o **terceiro container com `max-width + margin: 0 auto`** no projeto. Esse padrão de recorte e centralização é um dos fundamentos do layout web responsivo — vale fixar bem.

1. O logotipo do rodapé:

   ```css
   .footer-brand {
     font-size: 1.25rem;
     font-weight: 700;
     color: var(--color-text);
     text-decoration: none;
     letter-spacing: -0.05em;
   }
   ```

   - Propositalmente idêntico ao `.brand-link` da navbar em termos de tipografia. Isso reforça a consistência da identidade visual: o logotipo sempre aparece da mesma forma, independentemente de onde está na página.

1. Agora os links de navegação do rodapé:

   ```css
   .footer-nav {
     display: flex;
     flex-direction: row;
     gap: 2rem;
     flex-wrap: wrap;
     justify-content: center;
   }

   .footer-nav a {
     color: var(--color-text-muted);
     text-decoration: none;
     font-size: 0.875rem;
     font-weight: 500;
     transition: color 0.2s;
   }

   .footer-nav a:hover {
     color: var(--color-primary);
   }
   ```

   - **`flex-wrap: wrap`**: permite que os links quebrem para uma nova linha se a tela for muito estreita para exibi-los todos em uma só linha. Esta é uma preparação básica para responsividade.
   - **`justify-content: center`**: centraliza os links dentro do espaço disponível no Flexbox do `.footer-container`. Como o grupo do meio recebe o espaço "sobrado" após o brand e o copyright ocuparem os seus, esse `justify-content` garante que os links fiquem centralizados dentro desse espaço.
   - No hover, os links mudam para `--color-primary` (azul-lavanda), diferente dos links da navbar que mudam para branco. No rodapé, o uso da cor primária no hover cria um contraste agradável e um destaque sutil, sem competir com o conteúdo principal.

1. Por fim, o texto de copyright:

   ```css
   .footer-copy {
     font-size: 0.875rem;
     color: var(--color-text-muted);
     font-weight: 500;
     opacity: 0.8;
   }
   ```

   - **`opacity: 0.8`**: reduz ainda mais a visibilidade do copyright em relação ao restante do rodapé. Informações legais e de rodapé devem estar presentes, mas nunca competir com a atenção visual — uma opacidade levemente reduzida resolve isso com elegância.

1. O código final do `footer.css` deve ficar assim:

   ```css
   .site-footer {
     padding: 3rem;
     border-top: 1px solid var(--color-divisor);
   }

   .footer-container {
     display: flex;
     flex-direction: row;
     justify-content: space-between;
     align-items: center;
     max-width: var(--max-width-content);
     margin: 0 auto;
   }

   .footer-brand {
     font-size: 1.25rem;
     font-weight: 700;
     color: var(--color-text);
     text-decoration: none;
     letter-spacing: -0.05em;
   }

   .footer-nav {
     display: flex;
     flex-direction: row;
     gap: 2rem;
     flex-wrap: wrap;
     justify-content: center;
   }

   .footer-nav a {
     color: var(--color-text-muted);
     text-decoration: none;
     font-size: 0.875rem;
     font-weight: 500;
     transition: color 0.2s;
   }

   .footer-nav a:hover {
     color: var(--color-primary);
   }

   .footer-copy {
     font-size: 0.875rem;
     color: var(--color-text-muted);
     font-weight: 500;
     opacity: 0.8;
   }
   ```

---

### ✅ Resultado e próximos passos

- Ao abrir o `index.html` no navegador, você deve ver a seção hero com o título de grande impacto e os indicadores alinhados à sua base. Logo abaixo, o rodapé com a linha separadora sutil e os três grupos distribuídos horizontalmente.

- A estrutura do projeto `css/` está agora com quatro arquivos, cada um responsável por um componente do site:

  ```
  blogtech/
  ├── css/
  │   ├── style.css    → tokens globais e estilos base
  │   ├── navbar.css   → barra de navegação
  │   ├── hero.css     → seção hero
  │   └── footer.css   → rodapé
  └── index.html
  ```

- **Na próxima prática**, vamos implementar a seção principal da página: a grade de artigos (com cards de imagem) e a barra lateral (com a newsletter, categorias e autor em destaque). Os tokens de design definidos até agora (`--cor-primaria`, `--largura-max-conteudo`, `--cor-texto-suave`, entre outros) serão amplamente reutilizados — é aí que a estratégia de variáveis vai mostrar todo o seu valor.

- Se quiser se aprofundar nos conceitos trabalhados nesta prática, confira:
  - [align-items: flex-end — MDN Web Docs](https://developer.mozilla.org/pt-BR/docs/Web/CSS/align-items)
  - [flex-shrink — MDN Web Docs](https://developer.mozilla.org/pt-BR/docs/Web/CSS/flex-shrink)
  - [text-transform — MDN Web Docs](https://developer.mozilla.org/pt-BR/docs/Web/CSS/text-transform)
  - [Tipografia para web — web.dev](https://web.dev/articles/font-best-practices)
