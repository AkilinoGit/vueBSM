<script>
import axios from 'axios'
const apiurl = import.meta.env.VITE_BACKEND_IP
export default {
  name: 'FormOrg2',
  data() {
    return {
      formData: {
        km: null,
        loteId: null
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
        const response = await axios.put(apiurl + '/lote/transportarLote', this.formData)
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
  <h1>Org2</h1>
  <h2>Transportar Lote</h2>
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
        v-model="formData.km"
        @keyup.enter="handleSubmit"
        placeholder="Distancia (Km)"
      />
    </div>
    <button class="button-form green" type="submit">
      <span v-if="isSubmitting" class="loading-spinner"></span>
      <span v-else>CONFIRMAR</span>
    </button>
  </form>
</template>
