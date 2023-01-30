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
- Dentro da pasta *src* do ==React PLayground== crie um arquivo chamado ==*useClicks.js*==;
- No arquivo, crie uma função de mesmo nome, recebendo ==*value*== como input, ou parâmetro;
- Importe o hook nativo ==*useState*==, lembrando que o VScode pode fazer a importação automaticamente, à medida que se escreve.;
- Crie um hook para armazenar o valor do cliques e, como valor inicial, coloque o parâmetro, ou input, ==*value*==;
- Crie a função ==*handleClick*== e use o ==*setClick*== para incrementar o valor dos cliques;
- Retorne, em um objeto, tanto a variável ==*click*==, quanto a função ==*handleClick*==;

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
- Em ==*codeReview*==, inicie com o número dez;
##### Vamos para o retorno da função:
- Agora, tudo o que você precisa está dentro das constantes criadas anteriormente;
- Para o caso de **Aula ao vivo**, você usará ==*aula.handleClick*== no escutador de eventor ==*onCLick*== e ==*aula.click*== para mostrar seu valor;
- Para o caso de **Code Review**, você usará ==*codeReview.handleClick*== no escutador de eventor ==*onCLick*== e ==*codeReview.click*== para mostrar seu valor;
- Para o caso de **Exercícios**, você usará ==*exercicios.handleClick*== no escutador de eventor ==*onCLick*== e ==*exercicios.click*== para mostrar seu valor;