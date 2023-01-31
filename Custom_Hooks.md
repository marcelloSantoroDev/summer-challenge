

# Custom Hooks



### Depois de descobrir as maravilhas dos hooks nativos do React, como o *useState* e o *useEffect*, você deve estar pensando que não pode ficar melhor, não é? Mas fica.

### Os `Custom Hooks`, ou `Hooks Customizados`, vieram para trazer ainda mais dinamismo para suas aplicações, diminuindo a redundância e a complexidade em seus códigos. Bora lá conhecer esse novo amigo fiel.

#### O que vamos aprender?
- ##### O que são Hooks Customizados, entender porquê eles são tão bons para o desenvolvedor front-end e, finalmente, criar nossos próprios Hooks Customizados!

#### Você será capaz de:
- ##### Identificar redundância e complexidade no seu código com mais eficiência;
- ##### Criar Custom Hooks para diferentes ocasiões.

#### Por que isso é importante?
- ##### Uma das coisas essenciais para ser um bom profissional de desenvolvimento web é a capacidade de fazer do seu código o mais dinâmico, mais limpo e reutilizável possível. Os Hooks Customizados nos ajudam nessa ~~obrigação~~ tarefa.
- ##### Além disso, o uso de Hooks Customizados fortalece o senso de comunidade que devemos ter em nossas trajetórias no desenvolvimento web. Isso, porque há muitos Hooks Customizados já criados por outras pessoas e que você pode utilizar, assim como você poderá criar mais outros e disponibilizá-los para seus pares!

### Vamos juntes nessa viagem!!

![](https://media.giphy.com/media/l1J9xV815LOOTUju0/giphy.gif)






# Quando utilizar Custom Hooks?



#### Nas seções anteriores, você já aprendeu sobre as vantagens de se criar componentes genéricos e reutilizáveis em suas aplicações. Como, por exemplo, um componente de botão que você pode utilizar em mais de uma rota, apenas adaptando seus atributos para o contexto desejado.

#### Pois bem, um  Hook Customizado carrega exatamente esse benefício. É uma função genérica que utiliza `hooks nativos` para criar um`bloco de código` que exerce uma `lógica específica`, e pode ser utilizada em mais de um lugar da sua aplicação. Isso é vantajoso em diversos aspectos - você deixará seus componentes mais limpos e legíveis, diminuirá a complexidade do código e, principalmente, economizará tempo e energia para os problemas mais difíceis.

#### Vamos pensar em uma situação prática: suponhamos que você está trabalhando com mais de uma rota e, em cada uma delas, você precise fazer uma requisição para uma API diferente. Como nós faríamos isso da maneira que já aprendemos?

##### *Fique de olho!* :eyes:
- ##### esse exemplo pode ser bem útil para você ~~em projetos futuros~~ na sua carreira!

```JS
import React, { useState, useEffect } from 'react';

function App() {
  const [data, setData] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetch('https://api.imgflip.com/get_memes')
      .then(response => response.json())
      .then(data => {
        setData(data.data.memes);
        setLoading(false);
      });
  }, []);

  return (
    <div>
      { loading && <h1>Carregando...</h1> }
      { data.map((element) => (
        <div>
        <img key={element.id} src={element.url} alt={`meme ${element.id}`} width='500px'  />
        </div>
      )) }
    </div>
  );
}

export default App;
```

#### No código acima, nós estamos criando dois hooks nativos com o `useState` para armazenar os dados retornados da API e para "setar" o carregamento da página enquanto esta requisição não é finalizada. Logo abaixo, dentro de um `useEffect`, nós estamos fazendo a  requisição para uma API de memes e armazenando seus dados em `data`, bem como mudando o `loading` para falso. No retorno da função, estamos renderizando o texto "Carregando..." enquanto `loading` continua sendo `true` e, abaixo, fazendo um `map` nos itens retornados.

   `Um lembrete! O hook nativo useEffect, com seu array de dependências vazio, funciona de maneira similar ao o componentDidMount em componentes de classe.`

#### Essa maneira já é bem menos complexa do que com o uso dos estados em componentes de classe, mas dá para ficar muito melhor. No exemplo acima, toda a nossa lógica está na raiz da função do componente e não poderá ser reutilizada em outro lugar, além de prejudicar a limpeza das funções principais. Esse componente pode ficar limpinho, limpinho.

#### Com o uso de Hooks Customizados, nós podemos deixar a lógica reutilizável e movê-la para outro lugar. Podemos, por exemplo, criar uma pasta chamada `hooks` e, dentro dela, um arquivo chamado `useFetch.js`. O código ficaria assim:

```JS
import { useState, useEffect } from 'react';

export default function useFetch(url) {
  const [data, setData] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetch(url)
      .then(response => response.json())
      .then(fetchData => setData(fetchData))
    setLoading(false)
  }, [url]);

  return { data, loading };
}

```

#### Como você pode ver acima, nós separamos toda a lógica da requisição à API para o novo arquivo e retornamos o que vamos usar para colocá-la em prática.

#### Agora esse código, por ser dinâmico, além de estar separado da aplicação, pode ser usado para fazer requisições em outras rotas, para outras API's e armazenar seus dados para que possamos manipulá-los. Tudo isso sem precisar escrever mais linhas de código. Ou seja, `"por baixo dos panos"` :wink:

##### Agora, é só importar a função e aplicá-la em seu componente:

- Gaste alguns minutinhos tentando entender este código
```JS
import React from 'react';
import useFetch from './hooks/useFetch';

function App() {
const { data, loading } = useFetch('https://api.imgflip.com/get_memes');

  return (
    <div>
      { loading && <h1>Carregando...</h1> }
      <div>
      { data?.data.memes.map((element) => (
        <div>
        <img key={element.id} src={element.url} alt={`meme ${element.id}`} width='500px' />
        </div>
      )) }
      </div>
    </div>
  );
}

export default App;

```
- `Note¹`: o ponto de interrogação após **data** faz com que o **map** apenas aconteça se ele não for **null**, nem **undefined**`
- `Note²`: perceba que, em nosso componente, não precisamos mais usar **useEffect**, nem **useState**. O seu hook customizado está fazendo todo o trabalho por baixo dos panos.

#### No componente, estamos desestruturando a variável que vai armazenar o retorno da API, bem como a variável que vai "setar" o loading de `true` para `false`;

#### Estamos enviando a `url` da API para o parâmetro do hook customizado para que ele faça o seu trabalho corretamente;

#### Agora, é só pegar as variáveis `data` e `loading` e utilizá-las na renderização.

### Pronto! O seu componente está limpo, pouco complexo e você ainda tem uma função de requisições para usar outras vezes.

![](https://giphy.com/embed/SACoDGYTvVNhZYNb5a)
![mindblown](https://media.giphy.com/media/SACoDGYTvVNhZYNb5a/giphy.gif)

#### Muito legal, né? Então, partiu aprender a criar os nossos próprios Hooks Customizados? Partiu!






# Criando Custom Hooks



### A primeira lição do dia é: as duas regras de ouro dos Custom Hooks.

*Anota aí!* :pencil2: 

#### Primeira Regra:
- ##### Assim como utilizamos as extensões para identidicar arquivos `(ex: .js)`, ou as letras maiúsculas para identificar componentes React `(ex: App.js)`, nós devemos utilizar a palavra USE para indicar à nossa aplicação que o que estamos prestes a criar é, de fato, um Hook Customizado.
#### Segunda Regra:
- ##### Apenas é considerado Hook Customizado quando ele utiliza, em seu escopo, `hooks nativos` do React. Caso contrário, ele é apenas uma função genérica mesmo.

# *Show me the code!!!*

![show me the code](https://media.giphy.com/media/scZPhLqaVOM1qG4lT9/giphy.gif)

### Com essas duas regrinhas em mente, vamos começar a criar a nosso primeiro Hook Customizado! 

#### *Mas antes*, vá até o seu repositório de exercícios da trybe e, na respectiva seção, crie uma pasta para o dia de hoje.

##### Dentro dela, você irá rodar o seguinte comando:
```BASH
npx create-react-app custom-hooks
```

##### Após isso, você irá entrar na pasta criada:
```BASH
cd custom-hooks
```

##### Agora, é só abrir o seu VScode e colar esse código no arquivo App.js
```JS
import React, { useState } from 'react';

function App() {
  const [formData, setFormData] = useState({
    name: '',
    email: '',
    password: ''
  });

  const handleChange = (e) => {
    setFormData({
      ...formData,
      [e.target.name]: e.target.value
    });
  };

  return (
    <>
      <div>
        <input
          type="text"
          name="name"
          placeholder="Nome"
          value={formData.name}
          onChange={handleChange}
        />

      </div>
      <div>
        <input
          type="email"
          name="email"
          placeholder="Email"
          value={formData.email}
          onChange={handleChange}
        />

      </div>
      <div>
        <input
          type="password"
          name="password"
          placeholder="Senha"
          value={formData.password}
          onChange={handleChange}
        />

      </div>
      <button>
       Enviar
      </button>
     <h1>nome: { formData.name }</h1>
     <h1>email: { formData.email }</h1>
    </>
  );
}

export default App;
```

#### Esse é o mais que simples, mais que praticado, `handleChange` de um formulário.
- #### Estamos criando um hook com o `useState` e criando chaves para armazenar os dados que o usuário irá digitar nos *inputs*.
- #### Depois, criamos a nossa função `handleChange`, que vai ser utilizada no *escutador de eventos* `onChange`.

*Perceba que, no caso de componentes funcionais, é necessário fazer um "spread" do objeto antes de mudar as suas chaves dinamicamente, caso contrário, a sua função vai sobrescrever o que já foi armazenado*. 

#### Da maneira feita acima, a lógica só pode ser utilizada uma única vez. Será que podemos melhorar isso com um hook customizado?


![](https://media.giphy.com/media/nlSrYLgtOC0b2qxPfn/giphy.gif)
##### `Olha a dica!! Antes de avançar no conteúdo, tente pensar  em como implementar essa refatoração por conta própria` :wink:




#### Vamos ver o mesmo código, mas utilizando uma Hook Customizada:
- Na pasta src, crie outra pasta chamada `hooks`
- Dentro dela, crie um arquivo chamado `useFormValidation.js` e cole o seguinte código:

```JS
import { useState } from 'react';

export default function useFormValidation(initialState) {
  const [values, setValues] = useState(initialState);

  const handleChange = (e) => {
    setValues({
      ...values,
      [event.target.name]: e.target.value
    });
  };

  return {
    handleChange,
    values,
  };
}
```

#### Está criado o seu Custom Hook! Agora só falta refatorar o componente:
`antes de continuar, entenda plenamente o que foi feito acima`

```JS
import React from 'react';
import useFormValidation from './hooks/useFormValidation';

export default function LoginForm() {
  const {
    handleChange,
    values,
  } = useFormValidation({ name: '', email: '', password: '' });

  return (
    <>
          <input
        type="password"
        name="name"
        value={values.name}
        onChange={handleChange}
        placeholder='Nome'
      />
      <input
        type="email"
        name="email"
        value={values.email}
        onChange={handleChange}
        placeholder='Email'
      />

      <input
        type="password"
        name="password"
        value={values.password}
        onChange={handleChange}
        placeholder='senha'
      />
      <button>
        Enviar
     </button>
     <h1>Nome: {values.name}</h1>
     <h1>Email: {values.email}</h1>
    </>
  );
}
```

#### Reparou que o estado inicial também pode ser dinâmico? Dessa forma, estamos basicamente criando um `handleChange` que pode ser usado em qualquer outra situação de formulário.

#### Só precisamos fazer duas coisas:
-  *Desestruturar os valores que estão sendo retornados pelo hook customizado, para utilizá-los em nosso componente*;
- *Enviar, ao nosso custom hook, o estado inicial com o qual queremos trabalhar.*


![](https://media.giphy.com/media/yJFeycRK2DB4c/giphy.gif)

##### Vamos exercitar um pouquinho mais?






# Exercícios de fixação



### Para realizar o exercício, entre [nesse link](https://playcode.io/react) e cole, no arquivo *App.js*, o código abaixo:

```JS
import React from 'react';
import {useState} from 'react';

export function App() {
  const [aula, setAula] = useState(0);
  const [review, setReview] = useState(0);
  const [exercicios, setExercicios] = useState(0);

  const handleAulaClick = () => {
    setAula(aula + 1);
  }
  const handleReviewClick = () => {
    setReview(review + 1);
  }
  const handleExerciciosClick = () => {
    setExercicios(exercicios + 1);
  }

  return (
    <div className="App">
      <h1>Contador de Atividades</h1>
      <h3>Quantas vezes você realizou essas atividades hoje?</h3>

      <section className='atv-container'>

        <div>
        <button className='atv-1' onClick={handleAulaClick}>Aula ao vivo</button>
        <p>{aula}</p>
        </div>

        <div>
        <button className='atv-2' onClick={handleReviewClick}>Code Review</button>
        <p>{review}</p>
        </div>

        <div>
        <button className='atv-3' onClick={handleExerciciosClick}>Exercícios</button>
        <p>{exercicios}</p>
        </div>

      </section>
    </div>
  );
}
```

# Agora, é a sua vez!

![](https://media.giphy.com/media/3o6Ztn7QsncvRY58ty/giphy.gif)

#### Pense em como criar um Hook Customizado para esse caso - o de um contador. Ah, e faça com que o contador do `code review `comece a partir do número 10.

## Atenção! Para esse exercício, no `React Playground`, não crie pastas, crie apenas o arquivo do seu hook customizados direto na pasta src.
- sem estresse, viu? Qualquer coisa é só dar uma olhada *gabarito* :heart_eyes:






# Aula ao vivo



![](https://media.giphy.com/media/6wmz6Qo40eTDf4tW3Z/giphy.gif)

### Vamos para a aula ao vivo reforçar mais ainda os conceitos por trás sobre dessas belezinhas que são os Custom Hooks. :smile:






# Exercícios: agora a prática



### Para este exercício, vamos implementar um *ToggleTheme*. Nesse caso, é apenas um botão que muda de cor ao evento de clique.

### Na mesma aplicação React que você criou mais cedo, a *custom-hooks*, você terá que implementar a lógica *sem* custom hooks e, após isso, refatorar o código para usar a lógica *com* custom hook.

# Instruções

## Sem Custom Hook:

- Cole o seguinte código em seu arquivo `App.js`:
```JS

import React, { useState } from 'react';

const themes = {
  light: {
    background: "#eeeeee",
    text: "#000000"
  },
  dark: {
    background: "#000000",
    text: "#ffffff"
  }
};

function App() {
  return (
  <button>Mudar tema</button>
  );
}

export default App;
```

#### Use a constante `themes` para criar a lógica do seu toggle:
- Crie um hook com o `useState` para armazenar o valor alterável do seu tema de cor;
- Crie uma função `toggleTheme` para alterar o valor das cores de um para o outro;
- Por fim, implemente a lógica do seu `toggle` dentro do botão;
- Coloque, no `style` do botão, os valores de `cor de fundo (background)` e `cor de texto (text)` para habilitar o toggle, bem como `padding='100px'` e `fontSize='200px'` ;

*Dica: pesquise no google: como fazer estilizações 'inline'*.


## Com Custom Hook:

- Agora, pegue o código que você criou e tente refatorá-lo para utilizar um Hook Customizado;
- Na pasta `hooks`, crie o arquivo que armazenará o seu Custom Hook;
- Transfira a lógica do seu `toggle` para esse arquivo, criando uma função que fará o trabalho "por baixo dos panos";

*Dica: sua constante `themes` deverá ficar no escopo global do arquivo*

- No componente, importe a função e modifique o código para adaptá-lo ao seu Custom Hook;

##### Teste se funcionou. Caso tenha dificuldade, olhe a resolução no *gabarito*.

## Exercício bônus

#### Se você está com tempo, que tal tentar mais uma coisinha? Volte no primeiro código que vimos na aula, aquele da requisição à API  de memes, e tente adicionar um botão que salva a `url` dos memes que o usuário curtir:

- Crie um arquivo na pasta `hooks` chamado `useLocalStorage.js` e escreva a estrutura básica da sua função;
- `Dinamicamente`, crie a lógica que vai verificar se já existe algum valor em uma chave específica do `localStorage`. Se não existir, inicie essa chave com um array vazio;
- Armazene este valor em um hook, utilizando o `useState`;
- Use esse hook dentro de um `useEffect` para iniciar o `localStorage` com o valor desta constante à renderização do componente;
- Retorne, em um array, a variável que está armazenando o valor, bem como a função que o altera.

##### No componente:
- Importe o seu Hook Customizado;
- Desestruture o que foi retornado dele e envie para ele a chave para o localStorage, bem como um valor inicial;
- Crie uma função que ira incrementar os valores salvos no localStorage;
- Crie um botão com o texto `Curtir`;
- Adicione essa função no escutador de eventos `onClick` do botão, passando a `url`  da imagem como parâmetro;
*Dica: a função precisa ser executada com uma callBack*

#### A resolução está no *gabarito*.

![](https://media.giphy.com/media/JRU72sMVc3nLjrFA9I/giphy.gif)






# Recursos Adicionais



- [Sobre Custom Hooks no site do React](https://reactjs.org/docs/hooks-custom.html)
- [React Custom Hook tutorial with example](https://www.bezkoder.com/react-custom-hook/)
