
# Custom Hooks



#### Depois de descobrir as maravilhas dos hooks nativos do React, como o ==useState== e o ==useEffect==, você deve estar pensando que não pode ficar melhor, não é? Mas fica.

#### Os Custom Hooks, ou Hooks Customizados, vieram para trazer ainda mais dinamismo para suas aplicações, diminuindo a redundância e a complexidade em seus códigos. Bora lá conhecer esse novo amigo fiel.

### O que vamos aprender?
- ##### O que são Hooks Customizadas, entender porquê elas são tão boas para o desenvolvedor front-end e, finalmente, criar as nossas próprias Hooks Customizadas!

### Você será capaz de:
- ##### Identificar redundância e complexidade no seu código com mais eficiência;
- ##### Criar Custom Hooks para diferentes ocasiões.

### Por que isso é importante?
- ##### Uma das coisas essenciais para ser um bom profissional de desenvolvimento web é a capacidade de fazer do seu código o mais dinâmico, mais limpo e reutilizável possível. Os Hooks Customizados nos ajudam nessa ~~obrigação~~ tarefa.

### Vamos juntes nessa viagem!!

![](https://media.giphy.com/media/l1J9xV815LOOTUju0/giphy.gif)






# Quando utilizar Custom Hooks?



#### Nas seções anteriores, você já aprendeu sobre as vantagens de se criar componentes genéricos e reutilizáveis em suas aplicações, como, por exemplo, um componente de botão que você pode utilizar em mais de uma rota, apenas adaptando seus atributos para o contexto desejado.

#### Pois bem, uma Hook Customizada tem exatamente esse benefício. É uma função genérica que substitui hooks individuais e pode ser utilizada em mais de um lugar da sua aplicação. Isso é vantajoso em diversos aspectos - você deixará seus componentes mais limpos e legíveis, diminuir a complexidade do código e, principalmente, economizar tempo e energia para problemas mais difíceis.

###### *Fique de olho! 
- esse exemplo pode ser bem útil para você ~~em projetos futuros~~ na sua vida de desenvolvedor!

#### Vamos pensar em uma situação prática: suponhamos que você está trabalhando com mais de uma rota e, em cada uma delas, você precise fazer uma requisição para uma API diferente. Como nós faríamos isso da maneira que já aprendemos?

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
        <img key={element.id} src={element.url} alt={`meme ${element.id}`}  />
      )) }
    </div>
  );
}

export default App;

```

#### No código acima, nós estamos criando dois hooks nativos com o ==useState== para armazenar os dados retornados da API e para "setar" o carregamento da página enquanto essa requisição não é finalizada. Logo abaixo, dentro de um ==useEffect== nós estamos fazendo a  requisição para uma API de memes e armazenando seus dados em ==data==, bem como mudando o ==loading== para falso. No retorno da função, estamos renderizando o texto "Carregando..." enquanto ==loading== continua sendo true e, abaixo, fazendo um ==map== nos itens retornados.

 - *==Um lembrete! O hook nativo useEffect, com seu array de dependências vazio, funciona parecido com o componentDidMount em componentes de classe*

### Essa maneira já é bem menos complexa do que no uso dos estados em componentes de classe, mas dá para ficar muito melhor. No exemplo acima, toda a nossa lógica está na raiz da função do componente e não poderá ser reutilizada em lugar nenhum, além de prejudicar a limpeza das funções principais. Esse componente pode ficar limpinho, limpinho.

### Com o uso de Hooks Customizados, nós podemos deixar essa lógica reutilizável e movê-la para outro lugar. Podemos, por exemplo, criar um diretório chamado *hooks* e, dentro dele, criar um arquivo chamado ==useFetch.js==. O código ficaria assim:

```JS
import { useState, useEffect } from 'react';

export default function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetch(url)
      .then(response => response.json())
      .then(fetchData => setData(fetchData))
    setLoading(false)
  }, [url]);

  return [data, loading];
}

```

#### Como você pode ver acima, nós separamos toda a lógica da requisição à API para o novo arquivo. Agora, esse código, além de estar separado da aplicação, pode ser usado para fazer requisições em outras rotas, para outras API's e armazenar seus dados para que possamos manipulá-los. Tudo isso sem precisar escrever mais linhas de código!

##### Agora, é só importar a função e aplicá-la em seu componente:

```JS
import React from 'react';
import useFetch from './hooks/useTheme';

function App() {
const [data, loading] = useFetch('https://api.imgflip.com/get_memes');

  return (
    <div>
      { loading && <h1>Carregando...</h1> }
      { data?.data.memes.map((element) => (
        <img key={element.id} src={element.url} alt={`meme ${element.id}`}  />
      )) }
    </div>
  );
}

export default App;

```
- ==Note1: o ponto de interrogação após **data** faz com  que o **map** apenas aconteça se ele não for **null**, nem **undefined**
- ==Note2: perceba que, em nosso componente, não precisamos mais usar **useEffect**, ou **useState**. O seu hook customizado está fazendo todo o trabalho por baixo dos panos.

#### Pronto! Agora, o seu componente está limpo, pouco complexo e você ainda tem uma função de requisições para usar outras vezes.

![](https://giphy.com/embed/SACoDGYTvVNhZYNb5a)
![mindblown](https://media.giphy.com/media/SACoDGYTvVNhZYNb5a/giphy.gif)

#### Muito legal, né? Agora, partiu aprender a criar as nossas próprias Custom Hooks? Partiu!






# Criando Custom Hooks



#### A primeira lição do dia é: as duas regras de ouro dos Hooks Customizados.

#### Primeira Regra:
- ##### Assim como utilizamos as extensões para identidicar arquivos (ex: .js), ou as letras maiúsculas para identificar componentes React (ex: App.js), nós devemos utilizar a palavra USE para indicar à nossa aplicação que o que estamos prestes a criar é, de fato, um Hook Customizado.
#### Segunda Regra:
- ##### Apenas é considerado Hook Customizado quando ele utiliza, em seu escopo, hooks nativos do React. Caso contrário, ele é apenas uma função genérica mesmo.

## *Show me the code!!!*

![show me the code](https://media.giphy.com/media/scZPhLqaVOM1qG4lT9/giphy.gif)

#### Com essas duas regrinhas em mente, vamos começar a criar a nosso primeiro Hook Customizado! 

##### ==Mas antes==, vá até o seu repositório de exercícios da trybe e, na respectiva seção, crie uma pasta para o dia de hoje. Dentro dela, você irá rodar o seguinte comando:

```BASH
npx create-react-app custom-hooks
```

##### Após isso, você irá entrar na pasta criada:

```BASH
cd custom-hooks
```

#### Agora, é só abrir o seu VScode e colar esse código no arquivo App.js

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
          placeholder="Name"
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
          placeholder="Password"
          value={formData.password}
          onChange={handleChange}
        />

      </div>
      <button type="submit">
        Submit
      </button>
     <h1>nome: { formData.name }</h1>
     <h1>email: { formData.email }</h1>
    </>
  );
}

export default App;
```

### Esse é o mais que simples, mais que praticado, ==*handleChange*== de um formulário. Estamos criando um hook com o ==useState== e criando chaves para armazenar os dados que o usuário irá digitar nos *inputs*. Depois, criamos a nossa função ==handleChange==, que vai ser utilizada no escutador de eventos ==onChange==. <span style="color:green">Perceba que, no caso de componentes funcionais, é necessário fazer um "spread" do objeto antes de mudar as suas chaves dinamicamente, caso contrário, a sua função vai sobrescrever o que já foi armazenado</span>.  Da maneira feita acima, a lógica só pode ser utilizada uma única vez. Será que podemos pensar em fazer, dessa lógica, algo mais dinâmico?


![](https://media.giphy.com/media/nlSrYLgtOC0b2qxPfn/giphy.gif)
##### *Olha a dica!! Antes de avançar no conteúdo, tente pensar  em como implementar essa refatoração por conta própria ;)*




#### Vamos ver o mesmo código, mas utilizando uma Hook Customizada:
- Na pasta src, crie um diretório chamado ==**hooks**==
- Dentro dele, crie um arquivo chamado ==**useFormValidation**== e cole o seguinte código dentro dele:

```JS
import { useState } from 'react';

export default function useFormValidation(initialState) {
  const [values, setValues] = useState(initialState);

  const handleChange = (event) => {
    setValues({
      ...values,
      [event.target.name]: event.target.value
    });
  };

  return {
    handleChange,
    values,
  };
}
```

#### Está criado o seu Custom Hook! Agora só falta refatorar o componente:

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


![](https://media.giphy.com/media/yJFeycRK2DB4c/giphy.gif)

#### Vamos exercitar um pouquinho mais? Bora para os exercícios de fixação!






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

#### Pense em como criar um Hook Customizado para esse caso - o de um contador. Ah, e faça com que o contador do ==*code review*== começe a partir do número 10.

## Atenção! Para esse exercício no *React Playground*, não crie diretórios, crie apenas os arquivos necessários direto na pasta src.
- sem estresse, viu? Qualquer coisa é só dar uma olhada no <span style="color:green">gabarito</span> :))






# Aula ao vivo



![](https://media.giphy.com/media/6wmz6Qo40eTDf4tW3Z/giphy.gif)

### Vamos para a aula ao vivo reforçar mais ainda os conceitos por trás sobre dessas belezinhas, os Custom Hooks.






# Exercícios: agora a prática



### Para este exercício, vamos implementar um *ToggleTheme*. Nesse caso, é apenas um botão que muda de cor ao evento de clique.

### Na mesma aplicação React que você criou mais cedo, a *custom-hooks*, você terá que implementar a lógica <span style="color:red">sem</span> custom hooks e, após isso, refatorar o código para usar a lógica <span style="color:green">com</span> custom hook.

# Instruções


# Gabarito 

###### sem hooks
```JS

import React, { useState } from 'react';

function App() {

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

  const [theme, setTheme] = useState('light');

  const toggleTheme = () => {
    setTheme(theme === 'light' ? 'dark' : 'light');
  };

  return (
  <button
  onClick={toggleTheme}
  style={{ background: themes[theme].background, color: themes[theme].text, padding: '100px', fontSize: '200px' }}
  >Toggle Theme
  </button>
  );
}

export default App;
```

###### com hooks
- custom file
```JS
import { useState } from 'react';

  const themes = {
  light: {
    text: "#000000",
    background: "#eeeeee"
  },
  dark: {
    text: "#ffffff",
    background: "#222222"
  }
};

export default function useToggleTheme() {
  const [theme, setTheme] = useState(themes.light);

  const toggleTheme = () => {
    setTheme(theme === themes.light ? themes.dark : themes.light);
  };

  return [theme, toggleTheme];
}
```

- component file

```JS
import React from 'react';
import useToggleTheme from './hooks/useTheme';

function App() {

  const [theme, toggleTheme] = useToggleTheme();

  return (
  <button
  onClick={toggleTheme}
  style={{ background: theme.background, color: theme.text, padding: '100px', fontSize: '200px' }}
  >Toggle Theme
  </button>
  );
}

export default App;
```



![](https://media.giphy.com/media/JRU72sMVc3nLjrFA9I/giphy.gif)






# Recursos Adicionais



- [Sobre hooks customizados no site do React](**[https://reactjs.org/docs/hooks-custom.html](https://reactjs.org/docs/hooks-custom.html)**)
- [React Hooks: Organize sua Aplicação com Hooks Personalizados (Youtube)](**[https://www.youtube.com/watch?v=QjHX9qOngGA](https://www.youtube.com/watch?v=QjHX9qOngGA)**)
- [React Custom Hook tutorial with example](**[https://www.bezkoder.com/react-custom-hook/](https://www.bezkoder.com/react-custom-hook/)**)