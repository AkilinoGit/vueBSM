<script setup>
import FormOrg1 from './forms/FormOrg1.vue'
import FormOrg2 from './forms/FormOrg2.vue'
import FormOrg3 from './forms/FormOrg3.vue'
</script>
<script>
export default {
  props: {
    orgform: {
      type: String,
      required: true
    },
    updateResponse: {
      type: Function,
      required: true
    }
  },
  computed: {
    selectForm() {
      switch (this.orgform) {
        case 'Org1':
          return 'FormOrg1'
        case 'Org2':
          return 'FormOrg2'
        case 'Org3':
          return 'FormOrg3'
        default:
          return null
      }
    }
  },
  components: {
    FormOrg1,
    FormOrg2,
    FormOrg3
  },
  data() {
    return {
      response: 'Contenido inicial'
    }
  }
}
</script>
<template>
  <div class="orgsection">
    <component :is="selectForm" :updateResponse="updateResponse" />
  </div>
</template>
<style>
.orgsection {
  width: 70%;
  background-color: hsla(160, 100%, 37%, 1);
  border-radius: 5%;
}
h1,
h2 {
  text-align: center;
  color: black;
}
</style>
