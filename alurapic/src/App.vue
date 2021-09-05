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

<style></style>
