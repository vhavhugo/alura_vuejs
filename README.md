# alura_vuejs
Curso

# Auxilia criar um projeto do zero
npm install vue-cli@2.7.0 -g

# Criando um projeto
vue init webpack-simple alurapic

cd alurapic 
npm install
npm run dev

# Interpolação
<template>
  <div>
    <h1>Alurapic</h1>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        titulo: 'Alurapic',
      }
    }
  }
</script>

# Interpolação
# src/App.vue

<template>
  <div>
    <h1>Alurapic</h1>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        titulo: 'Alurapic',
      }
    }
  }
</script>

# Quando não é interpolação e sim atributo
<template>
  <div>
    <img :src="foto.url" :alt="foto.titulo" >
  </div>
</template>

<script>
  export default {
    data() {
      return {
        foto: {
          url: 'https://meupet.elanco.com/sites/g/files/adhwdz661/files/styles/paragraph_image/public/2020-04/bpc-48_-_filhotes.jpg',
          titulo: 'cachorro'
        }
      }
    }
  }
</script>

# usando mais de uma foto

<template>
  <div>
    <h1>{{ Alurapic }}</h1>
    <ul>
      <li v-for="foto of fotos">
        <img :src="foto.url" :alt="foto.titulo" >
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        titulo: 'Alurapic',
        fotos: [
          {
            url: 'https://meupet.elanco.com/sites/g/files/adhwdz661/files/styles/paragraph_image/public/2020-04/bpc-48_-_filhotes.jpg',
            titulo: 'cachorro'
          },
          {
            url: 'https://studiosol-a.akamaihd.net/tb/palcomp3-fotos/7/3/1/3/bailedocachorrao-ia-aa2b91971e814686a2251fc01c0eda10.jpg',
            titulo: 'cachorrão'
          }

        ]
      }
    }
  }
</script>

# Baixar pasta api do curso

entrar na pasta
npm start
localhost:3000/v1/fotos

# Como pegar a api e mostrar as fotos

1. Baixar modulo vue-resource
npm install vue-rosource@1.0.3 --save

2. Declarar no main.js
import VueResource from 'vue-resource';
Vue.use(VueResource);

# Criando um alert com componentes
<template>
  <div>
    <h1>{{ Alurapic }}</h1>
    <ul>
      <li v-for="foto of fotos">
        <img :src="foto.url" :alt="foto.titulo" >
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        titulo: 'Alurapic',
        fotos: []
      }
    },
    
    created() {
      alert('Criei componente');
    }
  }
</script>

# Integrando api de terceiros
<template>
  <div>
    <h1>{{ titulo }}</h1>
    <ul>
      <li v-for="foto of fotos">
        <img :src="foto.url" :alt="foto.titulo" >
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    data() {
      titulo: 'Alurapic'
      return {
        titulo: 'Alurapic',
        fotos: []
      }
    },

    created() {
      let promise = this.$http.get('http://localhost:3000/v1/fotos');
      promise
        .then(res => res.json())
        .then(fotos => this.fotos = fotos, err => console.log(err));
      }
    }
  
</script>

<style></style>

# estilizando
<template>
  <div class="corpo">
    <h1 class="centralizado">{{ titulo }}</h1>
    <ul class="lista-fotos">
      <li class="lista-fotos-item" v-for="foto of fotos">
        <div class="painel">
            <h2 class="painel-titulo">{{ foto.titulo }}</h2>
            <div class="painel-conteudo">
              <img class="imagem-responsiva" :src="foto.url" :alt="foto.titulo">
            </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    data() {
      titulo: 'Alurapic'
      return {
        titulo: 'Alurapic',
        fotos: []
      }
    },

    created() {
      let promise = this.$http.get('http://localhost:3000/v1/fotos');
      promise
        .then(res => res.json())
        .then(fotos => this.fotos = fotos, err => console.log(err));
      }
    }
  
</script>

<style>
  .corpo{
    font-family: Arial, Helvetica, sans-serif;
    width: 96%;
    margin: 0 auto;
  }
  .centralizado{
    text-align: center;
  }
  .lista-fotos{
    list-style: none;
  }
  .lista-fotos .lista-fotos-item{
    display: inline-block;
  }
  .imagem-responsiva{
    width: 100%;
  }
  /* estilo do painel */ 

   .painel {
    padding: 0 auto;
    border: solid 2px grey;
    display: inline-block;
    margin: 5px;
    box-shadow: 5px 5px 10px grey;
    width: 200px;
    height: 100%;
    vertical-align: top;
    text-align: center;
  }

  .painel .painel-titulo {
    text-align: center;
    border: solid 2px;
    background: lightblue;
    margin: 0 0 15px 0;
    padding: 10px;
    text-transform: uppercase;
  }
</style>

---------------------------------
As chances de querermos utilizar o mesmo painel em outras páginas da nossa aplicação não são pequenas. E para que isso seja possível, somos obrigados a copiar o código HTML e o CSS. Mesmo em uma aplicação Web tradicional na qual podemos importar o mesmo CSS em várias páginas, a marcação HTML terá que ser refeita.

Durante esse processo, essa ou aquela classe pode ser omitida ou essa ou aquela tag pode não ter sido fechada o que pode ocasionar problemas. Mais ainda, se a estrutura do painel mudar, seremos obrigados a alterar em todos os lugares. A boa notícia é que isso não precisa ser assim.

Podemos tornar nosso painel um componente de Vue e reutilizá-lo em qualquer outro local da nossa aplicação. Dizemos que nosso painel será um componente shared, compartilhado. O mesmo não ocorre com App.vue que é específico da nossa aplicação e não faz sentido ser reutilizado por outra aplicação ou ainda dentro da mesma aplicação.

Criando um shared component
Dessa forma, vamos criar a pasta alurapic/src/components/shared/painel. Todos nosso componentes que criarmos a partir de agora ficarão dentro da pasta components. Além disso, todos aqueles que forem componentes reutilizáveis e compartilháveis ficarão dentro da subpasta shared. Criaremos outra subpasta por componente e dentro dela teremos o arquivo .vue. Sendo assim vamos seguir a convenção de criar arquivos de componente começando em pascal case:

<!-- alurapic/src/components/shared/painel/Painel.vue -->

<template>
</template>

<script>

export default {
}
</script>
<style>
</style>COPIAR CÓDIGO
Agora que temos o esqueleto básico do nosso componente constituído pelas tags template, script e style, vamos mover a marcação do painel e seu estilo para dentro do componente:

<!-- alurapic/src/components/shared/painel/Painel.vue -->

<template>

    <div class="painel">

      <h2 class="painel-titulo"></h2>
      <div class="painel-conteudo">

      </div>
    </div>

</template>

<script>

export default {
}
</script>
<style>
 .painel {
    padding: 0 auto;
    border: solid 2px grey;
    display: inline-block;
    margin: 5px;
    box-shadow: 5px 5px 10px grey;
    width: 200px;
    height: 100%;
    vertical-align: top;
    text-align: center;
  }

  .painel .painel-titulo {
    text-align: center;
    border: solid 2px;
    background: lightblue;
    margin: 0 0 15px 0;
    padding: 10px;
    text-transform: uppercase;
  }

</style>COPIAR CÓDIGO
Nosso componente ainda não esta pronto, mas assim que estiver poderemos utilizá-lo em App.vue da seguinte maneira:

<!-- alurapic/src/App.vue -->

<template>
  <div class="corpo">

    <h1 class="centralizado">{{ titulo }}</h1>

    <ul class="lista-fotos">

      <li class="lista-fotos-item" v-for="foto in fotos">

        <meu-painel :titulo="foto.titulo">
          <img class="imagem-responsiva" :src="foto.url" :alt="foto.titulo">
        </meu-painel>

      </li>
    </ul>

  </div>
</template>
<!-- código posterior omitido -->COPIAR CÓDIGO
Veja como ficou simples a marcação do de App.vue. No caso, estamos usando o componente Painel.vue como meu-painel da definição do template de App.vue. Além disso, veja que o componente recebe seu título na propriedade titulo. Aliás, esse é um ponto que precisamos nos debruçar.

Todo componente em Vue é uma unidade de código que pode encapsular sua marcação, estilo e comportamento, este último, ações que podem ser realizadas com ele. Por enquanto, só disponibilizamos dados para o template e não executamos nenhum comportamento, algo que veremos ainda nesse curso.

Para que seja possível se comunicar com um componente passando dados para ele, precisamos adicionar a propriedade titulo na lista de propriedades recebíveis do componente App.vue. Alterando o componente:

<!-- alurapic/src/components/shared/painel/Painel.vue -->

<template>

  <div class="painel">

    <h2 class="painel-titulo">{{ titulo }}</h2>
    <div class="painel-conteudo">

    </div>
  </div>

</template>

<script>

export default {
   props: ['titulo']
}
</script>

<style>
 .painel {
    padding: 0 auto;
    border: solid 2px grey;
    display: inline-block;
    margin: 5px;
    box-shadow: 5px 5px 10px grey;
    width: 200px;
    height: 100%;
    vertical-align: top;
    text-align: center;
  }

  .painel .painel-titulo {
    text-align: center;
    border: solid 2px;
    background: lightblue;
    margin: 0 0 15px 0;
    padding: 10px;
    text-transform: uppercase;
  }

</style>COPIAR CÓDIGO
Veja que na parte scripts, temos a propriedade props. Nela podemos passar uma lista de propriedades que podem ser recebidas pelo componente. Essas propriedades podem ser acessadas no template do componente através de interpolação. É por isso que dentro da tag que representa o título do componente, usamos {{ titulo }}.

Com essa última alteração, nada será exibido em nosso navegador. Isto porque precisamos importar o componente Painel.vue em App.vue para poder utilizá-lo:

<!-- alurapic/src/App.vue -->
<template>
  <div class="corpo">

    <h1 class="centralizado">{{ titulo }}</h1>

    <ul class="lista-fotos">

      <li class="lista-fotos-item" v-for="foto in fotos">

        <meu-painel :titulo="foto.titulo">
          <img class="imagem-responsiva" :src="foto.url" :alt="foto.titulo">
        </meu-painel>

      </li>
    </ul>

  </div>
</template>

<script>

// importando nosso Painel 

import Painel from './components/shared/painel/Painel.vue';

export default {

  // código omitido
}
</script>
<style>

  /* estilos omitidos */

</style>COPIAR CÓDIGO
Importar nosso Painel ainda não é suficiente. Precisamos indicar em App.vue como iremos referenciar o componente em seu template. Podemos escolher qualquer nome, no caso, vamos escolher meu-painel. É através da propriedade components que associamos o nome meu-painel ao componente:

<!-- alurapic/src/App.vue -->

<script>
import Painel from './components/shared/painel/Painel.vue'

export default {

  components: {

    'meu-painel': Painel
  },

  data () {
    return {
      titulo: 'Alurapic', 

      fotos: []
    }
  },
  created() {

    this.$http
      .get('http://localhost:3000/v1/fotos')
      .then(res => res.json())
      .then(fotos => this.fotos = fotos, err => console.log(err));
  }
}
</script>
<style>

  /* estilos omitidos */

</style>COPIAR CÓDIGO
Excelente! Quando nosso página recarrega, temos um painel para cada foto. No entanto, apenas o título do painel é exibido. Onde está o seu conteúdo, no caso, nosso foto? Entenderemos o que houve no próximo vídeo.

Quando o Vue renderiza nosso componente Painel em App, ele não entende que deve preservar tudo aquilo que esta entre as tags <meu-painel>. O Vue manipula aquela parte do DOM trocando-a pela renderização do nosso componente Painel. Para que isso seja possível, precisamos indicar no template de Painel a área que queremos considerar como um slot, ou seja, aquela área que recebera tudo aquilo que tiver dentro da tag <meu-painel>. Para isso, vamos alterar o template alurapic/src/components/shared/painel/Painel.vue e trocar a div conteúdo pelo componente slot. Nosso componente final fica assim:

<!-- alurapic/src/components/shared/painel/Painel.vue -->

<template>

  <div class="painel">

    <h2 class="painel-titulo">{{ titulo }}</h2>
    <slot class="painel-conteudo">
    </slot>
  </div>

</template>

<script>

export default {
   props: ['titulo']
}
</script>

<style scoped>
 .painel {
    padding: 0 auto;
    border: solid 2px grey;
    display: inline-block;
    margin: 5px;
    box-shadow: 5px 5px 10px grey;
    width: 200px;
    height: 100%;
    vertical-align: top;
    text-align: center;
  }

  .painel .painel-titulo {
    text-align: center;
    border: solid 2px;
    background: lightblue;
    margin: 0 0 15px 0;
    padding: 10px;
    text-transform: uppercase;
  }

  * {
    box-shadow: 5px 5px 5px;
  }
</style>

Para saber mais: slots nomeados
PRÓXIMA ATIVIDADE

É possível termos mais de um slot por componente, por exemplo, para inserirmos conteúdo em locais diferentes do nosso componente. Para isso existe o named slot. Vejamos um exemplo:

<!-- ComponenteQualquer.vue -->
<template>
    <div>
        <slot name="cabecalho" class="header" ></slot>
        <hr>
        <slot class="body"></slot>
        <hr>
        <slot name="rodape" class="footer"></slot>
    </div>
</template>
<script>
export default {}
</script>COPIAR CÓDIGO
Veja que nosso componente possui três slots. Dois nomeados e outro não. Agora, quando ele for utilizado em outro componente podemos fazer:

<componente-qualquer>
    <div slot="cabecalho">
        <h1>Bem-vindo!</h1>
    </div>
    <p>Seja bem-vindo à Alura!</p>
    <div slot="rodape">
        <p>copyright 2017</p>
    </div>
</componente-qualquer>COPIAR CÓDIGO
As tag's divs que receberam a propriedade slot e seu nome, serão incluídas dentro do seu respectivo slot. Já o parágrafo Seja bem-vindo à Alura será inserido no slot padrão, aquele que não recebeu um nome em nosso componente.

