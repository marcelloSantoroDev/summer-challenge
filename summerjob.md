




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

### Vamos juntes nessa viagem!

![](https://media.giphy.com/media/l1J9xV815LOOTUju0/giphy.gif)


# Quando utilizar Custom Hooks?

###### *Fique de olho! 
- esse exemplo pode ser bem útil para você ~~em projetos futuros~~ na sua vida de desenvolvedor!

##### Nas seções anteriores, você já aprendeu sobre as vantagens de se criar componentes genéricos e reutilizáveis em suas aplicações, como, por exemplo, um componente de botão que você pode utilizar em mais de uma página, apenas adaptando seus atributos para o contexto certo.

##### Pois bem, uma Hook Customizada tem exatamente esse benefício. É uma função genérica que substitui hooks individuais e pode ser utilizada em mais de um lugar da sua aplicação.

##### Vamos pensar em uma situação prática. Suponhamos que você está trabalhando com mais de uma rota e, em cada uma delas, você precisa fazer uma requisição para uma API diferente. Como nós faríamos isso da maneira que já aprendemos?

```JS
// import React, { useState, useEffect } from 'react';

function App() {
  const [data, setData] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetch('https://jsonplaceholder.typicode.com/posts')
      .then(response => response.json())
      .then(data => {
        setData(data);
        setLoading(false);
      });
  }, []);

  return (
    <div>
      {loading ? (
        <p>Loading...</p>
      ) : (
        <ul>
          {data.map((item) => (
            <li key={item.id}>{item.title}</li>
          ))}
        </ul>
      )}
    </div>
  );
}

// export default App;

```


##### Dessa maneira, já bem menos complexo do que o uso dos estados em componentes de classe, mas dá para ficar muito melhor. No exemplo acima, toda a lógica está na raiz da função do componente e não poderá ser reutilizada em lugar nenhum, além de prejudicar a limpeza das funções principais.

##### Com o uso de Hooks Customizados, nós podemos fazer essa lógica reutilizável, movendo ela para outro lugar. Podemos, por exemplo, criar um diretório chamado *hooks* e, dentro dele, criar um arquivo chamado *useFetch.js*. O código ficaria assim:

```JS
// import { useState, useEffect } from 'react';

export default function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);

  async function fetchData() {
    const response = await fetch(url);
    const data = await response.json();
    setData(data);
    setLoading(false);
  }

  useEffect(() => {
    fetchData();
  }, []);

  return [data, loading];
}


```

##### Agora, esse código, além de estar separado da aplicação, pode ser usado para fazer requisições em outras rotas, armazenar os dados e manipulá-los, sem precisar escrever mais linhas de código!

##### Agora, é só importar a função e aplicá-la em seu componente

```JS
// import React from 'react';
// import useFetch from './useFetch';

function App() {
  const [data, loading] = useFetch('https://jsonplaceholder.typicode.com/posts');

  return (
    <div>
      {loading ? (
        <p>Loading...</p>
      ) : (
        <ul>
          {data.map((item) => (
            <li key={item.id}>{item.title}</li>
          ))}
        </ul>
      )}
    </div>
  );
}

// export default App;

```


![](https://giphy.com/embed/SACoDGYTvVNhZYNb5a)
![mindblown](https://media.giphy.com/media/SACoDGYTvVNhZYNb5a/giphy.gif)

##### Lega, né? Agora, partiu aprender a criar as nossas próprias Custom Hooks? Partiu!



# Criando Custom Hooks



##### A primeira lição do dia é: as duas regras de ouro das Hooks Customizadas.

#### Primeira Regra:
- ##### Assim como utilizamos as extensões para identidicar os arquivos (ex: .js), ou as letras maiúsculas para identificar componentes react (ex: App.js), nós devemos utilizar a palavra reservada USE para indicar à nossa aplicação que o que estamos prestes é criar é, de fato, uma hook customizada.
#### Segunda Regra:
- ##### Apenas é considerada uma Hook Customizada, quando ela utiliza, em seu escopo, hooks nativas do React. Caso contrário, ela é apenas uma função genérica mesmo

## *Show me the code!!!*

![show me the code](https://media.giphy.com/media/scZPhLqaVOM1qG4lT9/giphy.gif)

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

### Esse é o mais que simples, mais que praticado, *handleChange* de um formulário. No exemplo acima, essa lógica só pode ser utilizada uma única vez. Será que podemos pensar em fazer, dessa lógica, algo mais dinâmico?


![](https://media.giphy.com/media/nlSrYLgtOC0b2qxPfn/giphy.gif)
##### *Olha a dica!! Antes de avançar no conteúdo, tente pensar  em como implementar essa refatoração por conta própria ;)*

##### Agora, vamos ver o mesmo código, mas utilizando uma Hook Customizada:
- No diretório src, crie um diretório chamado **hooks**
- Dentro dele, crie um arquivo chamado **useFormValidation** e cole o seguinte código dentro dele:

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

###### Está criado o seu Custom Hook! Agora só falta refatorar o componente:

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

## Agora está na hora de exercitar!




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

#### Pense em como criar um Hook Customizado para esse caso, o de um contador. Ah, e faça com que o contador do *code review* começe a partir do npumero 10.

## Atenção! Para esse exercício, não crie diretórios no *React Playground*, crie apenas os arquivos necessários no diretório src.


- sem estresse, viu? Qualquer coisa é só dar uma olhada no <span style="color:red">gabarito</span> abaixo :))

##### Gabarito:
- *Exemplo para o hook customizado:*

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

- *Exemplo para o componente*

```JS
import React from 'react';
import {useState} from 'react';
import useClicks from './useClicks.js'

export function App() {
  const aula = useClicks(0);
  const review = useClicks(10);
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



# Aula ao vivo

### Vamos para a aula ao vivo reforçar mais ainda sobre essas belezinhas, as custom hooks :)


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



# Recursos Adicionais

- [Sobre hooks customizados no site do React](**[https://reactjs.org/docs/hooks-custom.html](https://reactjs.org/docs/hooks-custom.html)**)
- [React Hooks: Organize sua Aplicação com Hooks Personalizados (Youtube)](**[https://www.youtube.com/watch?v=QjHX9qOngGA](https://www.youtube.com/watch?v=QjHX9qOngGA)**)
- [React Custom Hook tutorial with example](**[https://www.bezkoder.com/react-custom-hook/](https://www.bezkoder.com/react-custom-hook/)**)

![](https://media.giphy.com/media/6wmz6Qo40eTDf4tW3Z/giphy.gif)