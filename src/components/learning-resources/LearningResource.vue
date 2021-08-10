<template>
    
    <li>
       <base-card>
            <header>
                <h3>{{name}}</h3>
                <base-button mode="flat" @click="deleteResource(id)"> Delete </base-button>
                 <base-button @click="toggelDetails" mode='flat'>
              {{ detailsAreVisible ? 'Hide' : 'Show' }} Details
             </base-button>
            </header>
           
             <p>{{phone}}</p>
                <p><b>Email:</b> {{email}}</p>
          
            
            
          <div v-if="detailsAreVisible">
            
            
              
                <p><b>Role:</b> {{role}}</p>
                <p><b>Signature:</b>{{signature}}</p>
                <p><b>Timezone:</b>{{timezone}}</p>
                
                  <nav>
                <a :href="url">Link</a>
            </nav>
          </div>
        </base-card>
    </li>
</template>

<script>
import BaseCard from '../UI/BaseCard.vue'
export default {
  components: { BaseCard },
     props:['id','phone','name','email','url','signature','role','timezone'],
     inject:['deleteResource'],
    data(){
      return {
        detailsAreVisible:false
      }
    },
    methods:{
       toggelDetails(){
            return this.detailsAreVisible = !this.detailsAreVisible;
        }
    }
}

</script>

<style scoped>
li {
  margin: auto;
  max-width: 40rem;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h3 {
  font-size: 1.25rem;
  margin: 0.5rem 0;
}

p {
  margin: 0.5rem 0;
}

a {
  text-decoration: none;
  color: #ce5c00;
}

a:hover,
a:active {
  color: #c89300;
}
</style>