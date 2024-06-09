<script setup>
import HelloWorld from './components/HelloWorld.vue'
import OrgSection from './components/OrgSection.vue'
import axios from 'axios'
</script>
<script>
const apiurl = import.meta.env.VITE_BACKEND_IP
export default {
  data() {
    return {
      response: {
        code: 'Bienvenido',
        data: 'Ejecute acción'
      },
      lotesList: []
    }
  },
  methods: {
    setResponse(code, data) {
      this.response['code'] = code == 1 ? 'ERROR' : 'SUCCESS'
      this.response['data'] = data
      this.setLotesList()
    },
    async setLotesList() {
      try {
        const response = await axios.get(apiurl + '/lote/listarLotes')
        console.log(response.data)
        this.lotesList = JSON.parse(JSON.parse(response.data['data']))
        console.log('lotesLIst var')
        console.log(this.lotesList)
      } catch (error) {
        console.error(error)
      }
    }
  }
}
</script>

<template>
  <header>
    <div class="wrapper">
      <HelloWorld msg="Veggie Supplie Chain Console" />
    </div>
  </header>
  <main>
    <div class="org-container">
      <OrgSection orgform="Org1" :updateResponse="setResponse" />
      <OrgSection orgform="Org2" :updateResponse="setResponse" />
      <OrgSection orgform="Org3" :updateResponse="setResponse" />
    </div>
    <div class="console-exit">
      <span>> {{ response['code'] }} </span>
      <br />
      <span>> {{ response['data'] }}</span>
    </div>
    <div class="mostrar-assets">
      <div class="fila-assets">
        <span class="border-title-asset">ID</span>
        <span class="border-title-asset">PRODUCTO</span>
        <span class="border-title-asset">ORIGEN</span>
        <span class="border-title-asset">KG</span>
        <span class="border-title-asset">KM</span>
        <span class="last-border-title-asset">PRECIO</span>
      </div>
      <div v-if="lotesList">
        <div v-for="(lote, index) in this.lotesList" :key="index">
          <div class="fila-assets">
            <span class="border-title-asset">{{ lote.id }}</span>
            <span class="border-title-asset">{{ lote.producto }}</span>
            <span class="border-title-asset">{{ lote.origen }}</span>
            <span class="border-title-asset">{{ lote.kg }}</span>
            <span class="border-title-asset">{{ lote.km }}</span>
            <span class="last-border-title-asset">{{ lote.precioKg }}</span>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.org-container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  margin-top: 20px;
  gap: 5px;
  justify-items: center;
  width: 70%;
  margin-inline: auto;
}
.console-exit {
  background-color: black;
  margin-top: 20px;
  width: 80%;
  margin-inline: auto;
  padding: 20px;
  border-color: hsla(160, 100%, 37%, 1);
  border-radius: 5px;
  color: hsla(160, 100%, 37%, 1);
}
.mostrar-assets {
  margin-top: 20px;
  padding: 20px;
  padding-top: 5px;
  background-color: hsla(160, 100%, 37%, 1);
  color: black;
}
.fila-assets {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr;
  text-align: right;
}
.fila-assets span {
  padding-right: 5px;
  font-weight: 600;
}
.border-title-asset {
  border-right: 1px solid black;
  border-bottom: 1px solid black;
}
.last-border-title-asset {
  border-bottom: 1px solid black;
}
</style>
