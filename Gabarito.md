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

#### Pense em como criar um Hook Customizado para esse caso - o de um contador. Ah, e faça com que o contador do *code review* começe a partir do número 10.

## Atenção! Para esse exercício no *React Playground*, não crie diretórios, crie apenas os arquivos necessários direto na pasta src.

##### *Custom Hook:*
```JS
import {useState} from 'react';

export default function useClicks (value) {
  const [click, setClick] = useState(value);

  const handleClick = () => {
    setClick(click + 1);
  }

  return {
    click,
    handleClick
  };
}
```
- Dentro da pasta *src* do `React PLayground` crie um arquivo chamado `useClicks.js`;
- No arquivo, crie uma função de mesmo nome, recebendo `value` como input, ou parâmetro;
- Importe o hook nativo `useState`, lembrando que o VScode pode fazer a importação automaticamente, à medida que se escreve.;
- Crie um hook para armazenar o valor do cliques e, como valor inicial, coloque o parâmetro, ou input, `value`;
- Crie a função `handleClick` e use o `setClick` para incrementar o valor dos cliques;
- Retorne, em um objeto, tanto a variável `click`, quanto a função `handleClick`;

##### *Componente:*
```JS
import React from 'react';
import useClicks from './useClicks.js'

export function App() {
  const aula = useClicks(0);
  const codeReview = useClicks(10);
  const exercicios = useClicks(0);

  return (
    <div className="App">
      <h1>Contador de Atividades</h1>
      <h3>Quantas vezes você realizou essas atividades hoje?</h3>

      <section className='atv-container'>

        <div>
        <button className='atv-1' onClick={aula.handleClick}>Aula ao vivo</button>
        <p>{aula.click}</p>
        </div>

        <div>
        <button className='atv-2' onClick={review.handleClick}>Code Review</button>
        <p>{review.click}</p>
        </div>

        <div>
        <button className='atv-3' onClick={exercicios.handleClick}>Exercícios</button>
        <p>{exercicios.click}</p>
        </div>

      </section>
    </div>
  );
}
```
- Importe o seu Hook Customizado no topo do arquivo;
- Crie três constantes, uma para cada tipo de atividade e armazene dentro delas, seu Hook Customizado;
- No input do seu hook, você vai determinar qual será o valor inicial de cada atividade;
- Em `codeReview`, inicie com o número dez;
##### Vamos para o retorno da função:
- Agora, tudo o que você precisa está dentro das constantes criadas anteriormente;
- Para o caso de **Aula ao vivo**, você usará `aula.handleClick` no escutador de eventos `onCLick` e `aula.click` para mostrar seu valor;
- Para o caso de **Code Review**, você usará `codeReview.handleClick` no escutador de eventor `onCLick` e `codeReview.click` para mostrar seu valor;
- Para o caso de **Exercícios**, você usará `exercicios.handleClick` no escutador de eventor `onCLick` e `exercicios.click` para mostrar seu valor;





# Exercícios: agora a prática



### Para este exercício, vamos implementar um *ToggleTheme*. Nesse caso, é apenas um botão que muda de cor ao evento de clique.

### Na mesma aplicação React que você criou mais cedo, a *custom-hooks*, você terá que implementar a lógica *sem* custom hooks e, após isso, refatorar o código para usar a lógica *com* custom hook.

# Instruções

## Sem Custom Hook:

- Cole o seguinte código em seu arquivo:
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

  return (
  <button>Toggle Theme</button>
  );
}

export default App;
```

#### Use a constante `themes` para criar a lógica do seu toggle:
- Crie um hook com o `useState` para armazenar o valor alterável do seu tema de cor;
- Crie uma função `toggleTheme` para alterar o valor das cores de um para o outro;
- Por fim, implemente a lógica do seu `toggle` dentro do botão;
- Coloque, no `style` do botão, os valores de `cor de fundo (background)` e `cor de texto (text)` para habilitar o toggle, nem como `padding='100px'` e `fontSize='200px'` ;
*Dica: pesquise no google: como fazer estilizações 'inline'*.


## Com Custom Hook:

- Agora, pegue o código que você criou e tente refatorá-lo para utilizar um Hook Customizado;
- Na pasta `hooks`, crie o arquivo que armazenará o seu Custom Hook;
- Transfira a lógica do seu `toggle` para esse arquivo, criando uma função que fará o trabalho "por baixo dos panos";
*Dica: sua constante `themes` deverá ficar no escopo global do arquivo*
- No componente, importe a função e modifique o código para adaptá-lo ao seu Custom Hook;

# Resolução

###### Sem Custom Hook:
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
  const [theme, setTheme] = useState(themes.light);

  const toggleTheme = () => {
    setTheme(theme === themes.light ? themes.dark : themes.light);
  };

  return (
  <button
  onClick={toggleTheme}
  style={{ background: theme.background, color: theme.text, padding: '100px', fontSize: '200px' }}
  >
  Mudar tema
  </button>
  );
}

export default App;
```
*A constante themes precisa estar no escopo global para que ela não seja recriada a cada renderização. Se esse fosse o caso, o nosso toggle não funcionaria corretamente*
- Crie um hook com o `useState` e coloque, como valor inicial, o tema `light`. Nesse momento, o seu hook `theme` estará armazenando o seguinte valor: `{ background: "#eeeeee", text: "#000000" } `
- Na sua função `toggleTheme`, use o `setTheme` para dizer que, a cada clique do botão, se o valor de `theme` for `themes.light`, você vai mudá-lo para `themes.dark` e vice-versa;
- Dentro do seu botão, adicione o escutdor de eventos `onClick` e coloque a sua função `toggleTheme` dentro dele.

###### Coloque também os atributos de estilização, para que o toggle funcione corretamente:
 - *em `background`, coloque o que estiver na chave `background` dentro do hook `theme`. Ou seja,  `theme.backgrouns`;*
 - Faça a mesma coisa para a cor do texto: `theme.text`


###### Com Custom Hook:

- Arquivo do Custom Hook:
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

  return{ theme, toggleTheme };
}
```
- Crie um arquivo na pasta `hooks` chamado `useToggleTheme`;
- Coloque a constante  `themes`, que estava no componente, no escopo global desse arquivo;
- Crie a função `toggleTheme`;
- Crie o hook que modificará o tema de cores do seu botão e armazese, como valor inicial, `themes.light` ;
- Crie a função `toggleTheme`, que se encarregará pela lógica da alternância de temas;
- Retorne, em um objeto, a variável `theme` e a função `toggleTheme`

- Arquivo do componente:
```JS
import React from 'react';
import useToggleTheme from './hooks/useTheme';

function App() {
  const { theme, toggleTheme } = useToggleTheme();

  return (
  <button
  onClick={toggleTheme}
  style={{ background: theme.background, color: theme.text, padding: '100px', fontSize: '200px' }}
  >
  Mudar tema
  </button>
  );
}

export default App;
```
- Importe a função `useToggleTheme` no topo do seu componente;
- Desestruture a variável `theme` e a função `toggleTheme`, retornados pelo seu hook customizado.





## Exercício bônus

#### Se você está com tempo, que tal tentar mais uma coisinha? Volte no primeiro código que vimos na aula, aquele da requisição à API  de memes, e tente adicionar um botão que salva a `url` dos memes que o usuário curtir:

- Crie um arquivo na pasta `hooks` chamado `useLocalStorage` e escreva a estrutura básica da sua função;
- Crie a lógica que vai verificar se já existe algo em uma chave específica e, se não existir, crie um valor padrão para iniciar essa chave no localStorage (tudo isso deve ser dinâmico e informado no `input` da função);
- Armazene o valor em uma variável;
- Crie o hook `useState` para guardar o valor;
- Use a variável desse hook dentro de um `useEffect` para "setar" o localStorage com o seu valor à renderização do componente;
- Retorne a variável que está armazenando o valor, bem como a função que o altera.
##### No componente:
- Importe o seu hook customizado;
- Desestruture o que foi retornado dele e crie uma chave para o localStorage, bem como um valor inicial;
- Crie uma função que ira incrementar os valores salvos no localStorage;
- Crie um botão com o texto `Curtir`;
- Adicione essa função no escutador de eventos `onClick` do botão, passando a url como parâmetro.
*Dica: a função precisa ser executada com uma callBack*

## Resolução:

- Arquivo do Custom Hook:
```JS
import { useState, useEffect } from 'react';

const useLocalStorage = (key, initialValue) => {
  const item = localStorage.getItem(key);
  const storedValue = item ? JSON.parse(item) : initialValue;
  const [value, setValue] = useState(storedValue);

  useEffect(() => {
    localStorage.setItem(key, JSON.stringify(value));
  }, [key, value]);

  return [value, setValue];
};

export default useLocalStorage;

```


- Arquivo do componente:
```JS
import React from 'react';
import useFetch from './hooks/useFetch';
import useLocalStorage from './hooks/useLocalStorage';

function App() {
  const [value, setValue] = useLocalStorage('likedMemes', []);
  const { data, loading } = useFetch('https://api.imgflip.com/get_memes');

  const handleLike = (url) => {
    setValue([...value, url]);
  };

  return (
    <div>
      {loading && <h1>Carregando...</h1>}
      <div>
        {data?.data.memes.map((element) => (
          <div>
            <img key={element.id} src={element.url} alt={`meme ${element.id}`} width="500px" />
            <div>
              <button
                style={{ width: '100px' }}
                value={element.url}
                onClick={() => handleLike(element.url)}
              >
                Curtir
              </button>
            </div>
          </div>
        ))}
      </div>
    </div>
  );
}

export default App;

```