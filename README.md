# Prática — Consumindo uma API com JavaScript

## 🎯 Objetivo

Nesta atividade vamos colocar em prática o consumo de uma API utilizando **JavaScript**.

Vamos criar uma página que consulta a **Random User API**, recebe uma lista de usuários e apresenta essas informações na tela.


```

---

# 1. Criando a pasta do projeto

Crie uma pasta para o projeto.

Por exemplo:

```text
random-user-api
```

Abra essa pasta no **Visual Studio Code**.

---

# 2. Criando os arquivos

Dentro da pasta, crie três arquivos:

```text
random-user-api/
│
├── index.html
├── app.js
└── style.css
```

Vamos começar pelo HTML.

---

# 3. Criando o HTML

Abra o arquivo:

```text
index.html
```

Digite:

```html
<!DOCTYPE html>
<html lang="pt-br">

<head>
    <meta charset="UTF-8">

    <meta name="viewport"
          content="width=device-width, initial-scale=1.0">

    <link rel="stylesheet" href="./style.css">

    <script src="./app.js" defer></script>

    <title>USERS</title>
</head>

<body>

</body>

</html>
```

### O que acabamos de fazer?

Criamos a estrutura básica da página.

Também fizemos duas ligações importantes:

```html
<link rel="stylesheet" href="./style.css">
```

Liga o CSS à página.

E:

```html
<script src="./app.js" defer></script>
```

Liga o JavaScript à página.

O `defer` faz com que o JavaScript aguarde o carregamento do HTML antes de ser executado.

---

# 4. Criando o cabeçalho

Dentro do `<body>`, vamos criar um `<header>`.

```html
<header>

    <h1>RANDOM USER GENERATOR API</h1>

</header>
```

O HTML agora fica:

```html
<body>

    <header>
        <h1>RANDOM USER GENERATOR API</h1>
    </header>

</body>
```

---

# 5. Criando o espaço para os usuários

Depois do `header`, vamos criar o `<main>`.

Dentro dele haverá uma `<div>` que receberá os usuários.

```html
<main>

    <div
        class="user-container"
        id="user-container">
    </div>

</main>
```

O código completo do `<body>` fica:

```html
<body>

    <header>
        <h1>RANDOM USER GENERATOR API</h1>
    </header>

    <main>

        <div
            class="user-container"
            id="user-container">
        </div>

    </main>

</body>
```

### Por que a `<div>` está vazia?

Porque **não vamos escrever os usuários manualmente no HTML**.

Eles serão criados pelo JavaScript depois que recebermos os dados da API.

---

# 6. Testando a página

Salve o arquivo.

Abra o `index.html` no navegador.

Por enquanto teremos apenas:

```text
RANDOM USER GENERATOR API
```

Ainda não temos usuários.

Isso é esperado.

---

# 7. Criando o JavaScript

Abra:

```text
app.js
```

Comece com:

```javascript
'use strict'
```

---

# 8. Criando a função responsável por buscar os usuários

Vamos criar uma função chamada `getUsers()`.

```javascript
async function getUsers() {

}
```

Essa função será responsável por **buscar os usuários na API**.

---

# 9. Informando o endereço da API

Dentro da função, crie uma variável chamada `url`:

```javascript
const url = 'https://randomuser.me/api/?results=8&nat=br'
```

Nossa função fica:

```javascript
async function getUsers() {

    const url =
        'https://randomuser.me/api/?results=8&nat=br'

}
```

Essa URL solicita:

* 8 usuários;
* utilizando `nat=br`.

---

# 10. Fazendo a requisição

Agora vamos utilizar o `fetch()`.

Adicione:

```javascript
const response = await fetch(url)
```

A função fica:

```javascript
async function getUsers() {

    const url =
        'https://randomuser.me/api/?results=8&nat=br'

    const response = await fetch(url)

}
```

Aqui estamos fazendo a requisição para a API.

---

# 11. Convertendo a resposta para JSON

Agora precisamos pegar os dados enviados pela API.

Adicione:

```javascript
const data = await response.json()
```

A função fica:

```javascript
async function getUsers() {

    const url =
        'https://randomuser.me/api/?results=8&nat=br'

    const response = await fetch(url)

    const data = await response.json()

}
```

---

# 12. Vamos verificar o que recebemos

Antes de continuar, vamos olhar os dados.

Adicione:

```javascript
console.log(data)
```

Fica:

```javascript
async function getUsers() {

    const url =
        'https://randomuser.me/api/?results=8&nat=br'

    const response = await fetch(url)

    const data = await response.json()

    console.log(data)
}
```

Mas ainda temos um problema.

Nossa função foi criada, mas **não foi chamada**.

---

# 13. Chamando a função

No final do arquivo:

```javascript
getUsers()
```

Agora abra o navegador e pressione:

```text
F12
```

Depois abra:

```text
Console
```

Você deverá visualizar a resposta da API.

---

# 14. Encontrando os usuários na resposta

Observe a resposta no console.

Você encontrará uma propriedade:

```text
results
```

É dentro dela que estão os usuários.

Então podemos retornar somente essa parte:

```javascript
return data.results
```

Nossa função fica:

```javascript
async function getUsers() {

    const url =
        'https://randomuser.me/api/?results=8&nat=br'

    const response = await fetch(url)

    const data = await response.json()

    return data.results
}
```

Agora nossa função retorna diretamente a lista de usuários.

---

# 15. Criando a função que vai carregar os usuários

Agora vamos criar outra função:

```javascript
async function loadUsers() {

}
```

Essa função será responsável por pegar os usuários e colocá-los na página.

---

# 16. Chamando `getUsers()`

Dentro de `loadUsers()`:

```javascript
const users = await getUsers()
```

Fica:

```javascript
async function loadUsers() {

    const users = await getUsers()

}
```

Agora temos:

```text
loadUsers()
    ↓
getUsers()
    ↓
fetch()
    ↓
API
    ↓
usuários
```

---

# 17. Verificando os usuários

Adicione:

```javascript
console.log(users)
```

Fica:

```javascript
async function loadUsers() {

    const users = await getUsers()

    console.log(users)

}
```

Agora precisamos chamar `loadUsers()`.

No final:

```javascript
loadUsers()
```

Temos:

```javascript
async function getUsers() {

    const url =
        'https://randomuser.me/api/?results=8&nat=br'

    const response =
        await fetch(url)

    const data =
        await response.json()

    return data.results
}


async function loadUsers() {

    const users =
        await getUsers()

    console.log(users)

}


loadUsers()
```

Abra o console.

Agora você verá um array contendo os usuários.

---

# 18. Pegando o container do HTML

Agora vamos parar de apenas mostrar os dados no console.

Precisamos colocar os usuários na página.

Primeiro vamos pegar a `<div>` que criamos no HTML.

```javascript
const userContainer =
    document.getElementById('user-container')
```

Coloque isso dentro de `loadUsers()`:

```javascript
async function loadUsers() {

    const users =
        await getUsers()

    const userContainer =
        document.getElementById('user-container')

}
```

Estamos dizendo ao JavaScript:

> Encontre no HTML o elemento que possui o ID `user-container`.

---

# 19. Percorrendo os usuários

Temos vários usuários dentro de:

```javascript
users
```

Precisamos trabalhar com cada um deles.

Vamos utilizar:

```javascript
users.forEach(user => {

})
```

Fica:

```javascript
async function loadUsers() {

    const users =
        await getUsers()

    const userContainer =
        document.getElementById('user-container')

    users.forEach(user => {

    })
}
```

Agora o JavaScript vai executar o código dentro do `forEach` uma vez para cada usuário.

---

# 20. Testando cada usuário

Antes de criar o HTML, vamos testar.

Dentro do `forEach`:

```javascript
console.log(user)
```

Fica:

```javascript
users.forEach(user => {

    console.log(user)

})
```

Abra o console.

Você verá cada usuário individualmente.

---

# 21. Criando um card

Agora vamos criar um elemento HTML para cada usuário.

Dentro do `forEach`:

```javascript
const card = document.createElement('article')
```

Estamos criando:

```html
<article></article>
```

O código fica:

```javascript
users.forEach(user => {

    const card =
        document.createElement('article')

})
```

---

# 22. Adicionando uma classe ao card

Vamos adicionar a classe:

```javascript
card.className = 'user-card'
```

Agora:

```javascript
users.forEach(user => {

    const card =
        document.createElement('article')

    card.className = 'user-card'

})
```

Essa classe será utilizada posteriormente pelo CSS.

---

# 23. Criando a imagem

Agora vamos criar os elementos filhos do card.

Começaremos pela imagem:

```javascript
const img = document.createElement('img')
```

Estamos criando:

```html
<img>
```

Agora vamos definir os atributos dela.

A URL está em:

```javascript
user.picture.large
```

Então:

```javascript
img.src = user.picture.large
img.alt = `Foto de ${user.name.first}`
img.className = 'user-image'
```

Fica assim:

```javascript
users.forEach(user => {

    const card =
        document.createElement('article')

    card.className = 'user-card'

    const img =
        document.createElement('img')

    img.src = user.picture.large
    img.alt = `Foto de ${user.name.first}`
    img.className = 'user-image'

})
```

---

# 24. Criando o elemento de nome

Agora vamos criar o `<h2>` para o nome:

```javascript
const name = document.createElement('h2')
```

Adicionamos a classe e o texto com o nome completo:

```javascript
name.className = 'user-name'
name.textContent = `${user.name.first} ${user.name.last}`
```

O código fica:

```javascript
users.forEach(user => {

    const card =
        document.createElement('article')

    card.className = 'user-card'

    const img =
        document.createElement('img')

    img.src = user.picture.large
    img.alt = `Foto de ${user.name.first}`
    img.className = 'user-image'

    const name =
        document.createElement('h2')

    name.className = 'user-name'
    name.textContent =
        `${user.name.first} ${user.name.last}`

})
```

Aqui usamos `textContent` para colocar apenas texto dentro do `<h2>`, sem interpretar como HTML.

---

# 25. Adicionando o e-mail

Agora vamos criar o `<p>` para o e-mail:

```javascript
const email = document.createElement('p')
email.textContent = user.email
```

---

# 26. Adicionando o telefone

E o `<p>` para o telefone:

```javascript
const cell = document.createElement('p')
cell.textContent = user.cell
```

---

# 27. Montando o card

Agora que todos os elementos foram criados, precisamos colocá-los **dentro** do card.

Usamos `appendChild()` para anexar cada filho ao card:

```javascript
card.appendChild(img)
card.appendChild(name)
card.appendChild(email)
card.appendChild(cell)
```

O código dentro do `forEach` fica:

```javascript
users.forEach(user => {

    const card =
        document.createElement('article')

    card.className = 'user-card'

    const img =
        document.createElement('img')

    img.src = user.picture.large
    img.alt = `Foto de ${user.name.first}`
    img.className = 'user-image'

    const name =
        document.createElement('h2')

    name.className = 'user-name'
    name.textContent =
        `${user.name.first} ${user.name.last}`

    const email =
        document.createElement('p')

    email.textContent = user.email

    const cell =
        document.createElement('p')

    cell.textContent = user.cell

    card.appendChild(img)
    card.appendChild(name)
    card.appendChild(email)
    card.appendChild(cell)

})
```

---

# 28. Colocando o card na página

Até agora criamos o card e seus filhos, mas eles ainda estão apenas na memória do navegador.

Precisamos adicioná-los ao container da página.

Depois de anexar os filhos ao card:

```javascript
userContainer.appendChild(card)
```

Agora o card será colocado dentro da:

```html
<div id="user-container">
```

---

# 29. Função `loadUsers()` completa

Nossa função `loadUsers()` ficou assim:

```javascript
async function loadUsers() {

    const users =
        await getUsers()

    const userContainer =
        document.getElementById('user-container')

    users.forEach(user => {

        const card =
            document.createElement('article')

        card.className = 'user-card'

        const img =
            document.createElement('img')

        img.src = user.picture.large
        img.alt = `Foto de ${user.name.first}`
        img.className = 'user-image'

        const name =
            document.createElement('h2')

        name.className = 'user-name'
        name.textContent =
            `${user.name.first} ${user.name.last}`

        const email =
            document.createElement('p')

        email.textContent = user.email

        const cell =
            document.createElement('p')

        cell.textContent = user.cell

        card.appendChild(img)
        card.appendChild(name)
        card.appendChild(email)
        card.appendChild(cell)

        userContainer.appendChild(card)

    })
}
```

---

# 30. Por que `createElement` e não `innerHTML`?

Usar `createElement` e `appendChild` é uma forma **mais segura e estruturada** de construir elementos HTML pelo JavaScript.

Vantagens:

* **Segurança:** evita injeção de código malicioso, pois não interpretamos strings como HTML.
* **Organização:** cada elemento é uma variável, fácil de manipular depois.
* **Clareza:** o código mostra exatamente o que está sendo criado.

---

# 31. JavaScript completo

Neste momento, nosso JavaScript está pronto:

```javascript
'use strict'


async function getUsers() {

    const url =
        'https://randomuser.me/api/?results=8&nat=br'

    const response =
        await fetch(url)

    const data =
        await response.json()

    return data.results
}


async function loadUsers() {

    const users =
        await getUsers()

    const userContainer =
        document.getElementById('user-container')

    users.forEach(user => {

        const card =
            document.createElement('article')

        card.className = 'user-card'

        const img =
            document.createElement('img')

        img.src = user.picture.large
        img.alt = `Foto de ${user.name.first}`
        img.className = 'user-image'

        const name =
            document.createElement('h2')

        name.className = 'user-name'
        name.textContent =
            `${user.name.first} ${user.name.last}`

        const email =
            document.createElement('p')

        email.textContent = user.email

        const cell =
            document.createElement('p')

        cell.textContent = user.cell

        card.appendChild(img)
        card.appendChild(name)
        card.appendChild(email)
        card.appendChild(cell)

        userContainer.appendChild(card)

    })
}


loadUsers()
```

Abra o navegador.

Os usuários já devem aparecer.

---

# 32. Agora vamos cuidar do visual

O consumo da API já está funcionando.

A partir daqui, vamos apenas melhorar a apresentação.

Abra:

```text
style.css
```

---

# 33. Reset básico

Comece com:

```css
* {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
}
```

Isso remove espaçamentos padrão do navegador.

---

# 34. Configurando o `body`

Adicione:

```css
body {
    display: flex;
    flex-direction: column;
    background-color: #eee;
}
```

---

# 35. Formatando o cabeçalho

Adicione:

```css
header {
    height: 100px;

    display: flex;

    justify-content: center;

    align-items: center;

    color: #666;

    text-align: center;
}
```

---

# 36. Organizando os usuários

Agora vamos transformar o container em uma grade.

```css
.user-container {
    display: grid;

    grid-template-columns:
        repeat(auto-fit, minmax(300px, 1fr));

    padding-inline: 12vw;

    user-select: none;
}
```

O `grid` permitirá organizar os usuários em colunas.

O `auto-fit` e o `minmax()` ajudam a fazer o layout se adaptar ao tamanho da tela.

---

# 37. Formatando os cards

Adicione:

```css
.user-card {
    display: flex;

    flex-direction: column;

    justify-content: center;

    align-items: center;

    gap: 8px;

    aspect-ratio: 1;

    width: 100%;

    box-shadow: 0 0 1px #666;

    cursor: pointer;

    transition: .5s;
}
```

---

# 38. Criando o efeito ao passar o mouse

Adicione:

```css
.user-card:hover {
    box-shadow: 0 0 32px #666;
}
```

Agora, quando o mouse passar sobre o card, ele terá um efeito visual.

---

# 39. Formatando a imagem

Para deixar a imagem redonda:

```css
.user-image {
    border-radius: 50%;

    border: 2px solid #666;

    padding: 6px;
}
```

---

# 40. Deixando os textos mais suaves

Por fim:

```css
p {
    color: #666;
}
```

---

# 41. CSS completo

Ao final:

```css
* {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
}

body {
    display: flex;
    flex-direction: column;
    background-color: #eee;
}

header {
    height: 100px;

    display: flex;

    justify-content: center;

    align-items: center;

    color: #666;

    text-align: center;
}

.user-container {
    display: grid;

    grid-template-columns:
        repeat(auto-fit, minmax(300px, 1fr));

    padding-inline: 12vw;

    user-select: none;
}

.user-card {
    display: flex;

    flex-direction: column;

    justify-content: center;

    align-items: center;

    gap: 8px;

    aspect-ratio: 1;

    width: 100%;

    box-shadow: 0 0 1px #666;

    cursor: pointer;

    transition: .5s;
}

.user-card:hover {
    box-shadow: 0 0 32px #666;
}

.user-image {
    border-radius: 50%;

    border: 2px solid #666;

    padding: 6px;
}

p {
    color: #666;
}
```

---

# 42. Projeto final

Ao final teremos:

```text
random-user-api/
│
├── index.html
├── app.js
└── style.css
```

## `index.html`

```html
<!DOCTYPE html>
<html lang="pt-br">

<head>
    <meta charset="UTF-8">

    <meta
        name="viewport"
        content="width=device-width,
                 initial-scale=1.0">

    <link
        rel="stylesheet"
        href="./style.css">

    <script
        src="./app.js"
        defer>
    </script>

    <title>USERS</title>
</head>

<body>

    <header>
        <h1>RANDOM USER GENERATOR API</h1>
    </header>

    <main>

        <div
            class="user-container"
            id="user-container">
        </div>

    </main>

</body>

</html>
```

---

# 43. O que acontece quando abrimos a página?

Agora conseguimos acompanhar o funcionamento do projeto.

### 1. O navegador carrega o HTML

```text
index.html
```

### 2. O JavaScript é carregado

```text
app.js
```

### 3. `loadUsers()` é executado

```javascript
loadUsers()
```

### 4. `getUsers()` é executado

```javascript
const users = await getUsers()
```

### 5. O `fetch()` faz a requisição

```javascript
fetch(url)
```

### 6. A API responde

```text
Random User API
       ↓
      JSON
```

### 7. Transformamos a resposta

```javascript
response.json()
```

### 8. Pegamos os usuários

```javascript
data.results
```

### 9. Percorremos os usuários

```javascript
users.forEach(...)
```

### 10. Criamos um card para cada usuário

```javascript
document.createElement('article')
```

### 11. Criamos e anexamos os filhos do card

```javascript
card.appendChild(img)
card.appendChild(name)
card.appendChild(email)
card.appendChild(cell)
```

### 12. Inserimos o card no HTML

```javascript
userContainer.appendChild(card)
```

O fluxo completo:

```text
API
 ↓
dados
 ↓
JavaScript (createElement + appendChild)
 ↓
HTML
 ↓
usuários na tela
```

---

# 44. Testando o consumo da API

Agora vamos modificar o projeto para observar o comportamento da API.

## Teste 1 — quantidade de usuários

Altere:

```text
results=8
```

para:

```text
results=3
```

Atualize a página.

Depois teste:

```text
results=15
```

Observe o resultado.

---

# 45. Teste 2 — mostrando somente o nome

Remova temporariamente:

```javascript
const email =
    document.createElement('p')

email.textContent = user.email

const cell =
    document.createElement('p')

cell.textContent = user.cell

card.appendChild(email)
card.appendChild(cell)
```

Atualize a página.

Observe o resultado.

---

# 46. Teste 3 — adicionando uma nova informação

Escolha outra informação disponível no usuário.

Primeiro encontre a propriedade no console.

Depois utilize `createElement` e `textContent`:

```javascript
const novaInfo = document.createElement('p')
novaInfo.textContent = user.propriedade

card.appendChild(novaInfo)
```

O objetivo é localizar uma informação na resposta da API e utilizá-la no HTML.

---

# 47. Teste 4 — explorando o objeto

Adicione novamente:

```javascript
console.log(user)
```

Abra o console do navegador e explore o objeto.

Tente encontrar:

```text
nome
sobrenome
email
telefone
imagem
```

---

# 48. Desafio final

Agora faça uma alteração sem seguir o passo a passo.

Modifique o projeto para mostrar **mais uma informação do usuário**.

Siga o processo:

```text
1. Consultar o objeto no console
          ↓
2. Encontrar a propriedade
          ↓
3. Criar o elemento com createElement
          ↓
4. Atribuir o valor com textContent
          ↓
5. Anexar ao card com appendChild
          ↓
6. Verificar no navegador
```

---

# 🎯 Resultado esperado

Ao finalizar a prática, o projeto deverá:

1. Fazer uma requisição para a API;
2. Receber os usuários;
3. Percorrer os dados recebidos;
4. Criar os elementos HTML dinamicamente usando **`createElement` e `appendChild`**;
5. Exibir os dados na página;
6. Permitir que você altere e explore os dados retornados pela API.

**O objetivo principal não é o layout dos usuários. O objetivo é praticar o processo completo de consumir uma API utilizando JavaScript, construindo a interface de forma segura e estruturada através do DOM.**
# ATIVIDADE-API-USER
