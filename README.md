# Custom Hooks



##### Depois de descobrir as maravilhas dos hooks nativos, você deve estar pensando que não pode ficar melhor, não é? Mas fica.

##### As Custom Hooks, ou Hooks Customizadas, vieram para trazer ainda mais dinamismo para suas aplicações, diminuindo a redundância e a complexidade em seus códigos. Bora lá conhecer esse novo amigo fiel.

### O que vamos aprender?
- ##### O que são Hooks Customizadas, entender porquê elas são tão boas para o dev front-end e, finalmente, criar as nossas próprias Hooks Customizadas!

### Você será capaz de:
- ##### Identificar redundância e complexidade no seu código.
- ##### Criar Custom Hooks

### Por que isso é importante?
- ##### Uma das coisas essenciais para ser um bom profissional de desenvolvimento web é ser capaz de fazer do seu código o mais dinâmico, mais limpo e reutilizável possível. As Hooks Customizadas nos ajudam nessa tarefa.

# Quando utilizar Custom Hooks?



##### Nas seções anteriores, você já aprendeu sobre as vantagens de se criar componentes genéricos e reutilizáveis em suas aplicações, como, por exemplo, um componente de botão que você pode utilizar em mais de uma página, apenas adaptando seus atributos para o contexto certo.

##### Pois bem, uma Hook Customizada tem exatamente esse benefício. É uma função genérica que substitui hooks individuais e pode ser utilizada em mais de um lugar da sua aplicação.

##### Por exemplo: vamos pensar naquele botão componentizado, que pode ser utilizado em mais de um lugar. 

```JS
Colocar o exemplo aqui
```

##### No seu evento de clique, nós podemos criar uma hook customizada para realizar uma ação que pode ser repetida em outro lugar da sua aplicação

```JS
Colocar o exemplo aqui
```

# Criando Custom Hooks



##### A primeira lição do dia é: as duas regras de ouro das Hooks Customizadas.

#### Primeira Regra:
- ##### Assim como utilizamos as extensões para identidicar os arquivos (ex: .js), ou as letras maiúsculas para identificar componentes react (ex: App.js), nós devemos utilizar a palavra reservada USE para indicar à nossa aplicação que o que estamos prestes é criar é, de fato, uma hook customizada.
#### Segunda Regra:
- ##### Apenas é considerada uma Hook Customizada, quando ela utiliza, em seu escopo, hooks nativas do React. Caso contrário, ela é apenas uma função genérica mesmo

## Show me the code!
```JS
Adicionar GIF aqui
```

##### Com essas duas regrinhas em mente, vamos começar a criar a nossa primeira Hook Customizada! 

###### Mas antes, vá até o seu repositório de exercícios da trybe e, na respectiva seção, crie uma pasta para o dia de hoje. Dentro dela, você irá rodar o seguinte comando:

```BASH
npx create-react-app custom-hooks
```

##### Após isso, você irá entrar na pasta criada:

```BASH
cd custom-hooks
```

#### Agora, é só abrir o seu VScode e colar esse código no arquivo App.js

```JS
Colocar o código aqui
```

# explicar exemplo do código sem custom hook

##### Agora, vamos ver o mesmo código, mas utilizando uma Hook Customizada:

```JS
Colocar o código aqui
```

##### Dessa maneira, nós conseguimos limpar o componente e, ainda por cima, criamos uma função que pode nos ajudar em outros componentes. Legal, né?
