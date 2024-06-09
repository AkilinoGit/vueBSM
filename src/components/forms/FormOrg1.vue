<script>
import axios from 'axios'
const apiurl = import.meta.env.VITE_BACKEND_IP
export default {
  name: 'FormOrg1',
  data() {
    return {
      formData: {
        kg: null,
        loteId: null,
        origen: '',
        producto: ''
      },
      isSubmitting: false
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
        const response = await axios.post(apiurl + '/lote/registrarLote', this.formData)
        console.log(response.data)
        this.updateResponse(response.data['code'], response.data['data'])
      } catch (error) {
        console.error(error)
      } finally {
        this.isSubmitting = false
      }
    }
  }
}
</script>
<template>
  <h1>Org1</h1>
  <h2>Registrar Lote</h2>
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
        v-model="formData.producto"
        @keyup.enter="handleSubmit"
        placeholder="Producto"
      />
    </div>
    <div class="around-input">
      <input
        class="green"
        v-model="formData.origen"
        @keyup.enter="handleSubmit"
        placeholder="Origen"
      />
    </div>
    <div class="around-input">
      <input
        class="green"
        v-model="formData.kg"
        @keyup.enter="handleSubmit"
        placeholder="Cantidad (Kg)"
      />
    </div>
    <button class="button-form green" type="submit">
      <span v-if="isSubmitting" class="loading-spinner"></span>
      <span v-else>REGISTRAR</span>
    </button>
  </form>
</template>
