<script>
import axios from 'axios'
const apiurl = import.meta.env.VITE_BACKEND_IP
export default {
  name: 'FormOrg3',
  data() {
    return {
      formData: {
        loteId: null,
        precioKg: ''
      },
      formVenta: {
        loteId: ''
      },
      isSubmitting: false,
      isDeleting: false
    }
  },
  props: {
    updateResponse: {
      type: Function,
      required: true
    }
  },
  methods: {
    async handleSubmit() {
      this.isSubmitting = true
      try {
        const response = await axios.put(apiurl + '/lote/venderLote', this.formData)
        console.log(response.data)
        this.updateResponse(response.data['code'], response.data['data'])
      } catch (error) {
        console.error(error)
      } finally {
        this.isSubmitting = false
      }
    },
    async eliminarLote() {
      this.isDeleting = true
      try {
        console.log(apiurl + '/lote/loteVendido?loteId=' + this.formVenta.loteId)
        const response = await axios.delete(
          apiurl + '/lote/loteVendido?loteId=' + this.formVenta.loteId
        )

        console.log(response.data)
        this.updateResponse(response.data['code'], response.data['data'])
      } catch (error) {
        console.error(error)
      } finally {
        this.isDeleting = false
      }
    }
  }
}
</script>
<template>
  <h1>Org3</h1>
  <h2>Poner en venta</h2>
  <form class="form" @submit.prevent="handleSubmit">
    <div class="around-input">
      <input
        class="green"
        v-model="formData.loteId"
        @keyup.enter="handleSubmit"
        placeholder="Lote ID"
      />
    </div>
    <div class="around-input">
      <input
        class="green"
        v-model="formData.precioKg"
        @keyup.enter="handleSubmit"
        placeholder="Precio/Kg (€)"
      />
    </div>
    <button class="button-form green" type="submit">
      <span v-if="isSubmitting" class="loading-spinner"></span>
      <span v-else>CONFIRMAR</span>
    </button>
  </form>
  <h2>Lote Vendido</h2>
  <form class="form" @submit.prevent="eliminarLote">
    <div class="around-input">
      <input
        class="green"
        v-model="formVenta.loteId"
        @keyup.enter="eliminarLote"
        placeholder="Identificador"
      />
    </div>
    <button class="button-form green" type="submit">
      <span v-if="isDeleting" class="loading-spinner"></span>
      <span v-else>CONFIRMAR</span>
    </button>
  </form>
</template>
