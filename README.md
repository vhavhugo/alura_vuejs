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

