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
