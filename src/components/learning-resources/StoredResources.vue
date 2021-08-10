<template>
      <ul>
      
      <LearningResource 
        v-for="res in resources" 
        :key="res.id" 
        :id="res.id"
        :name="res.name"
        :phone="res.phone"
        :email="res.email"
         :signature="res.signature"
        :role="res.role"
        :url="res.url"
        :timezone="res.timezone"
        >
      </LearningResource>
      
    </ul>
</template>

<script>
import LearningResource from './LearningResource'
export default {
  inject:['$resources'],
  computed: {
    resources() {
      return this.$resources()
    }
  },
  components:{
      LearningResource
  },
}
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>