<template>
 <base-card>
        <div class="form-control">
                <label for="link">User Search</label>
                <input id="searchQuery" name="searchQuery" type="text" v-model="searchQuery" />
        </div>
                    <div class="form-control">
                <tbody> 
                    <!-- <tr v-for="item in resultQuery" :key="item.id">
                        <td><a v-bind:href="item.name" target="_blank">{{item.name}}</a></td>
                    </tr> -->
                </tbody>
                 </div>
  </base-card>

    <base-card>
        <base-button @click="setSelectedTab('stored-resources')" :mode="storedResButtonMode">User List</base-button>
        <base-button @click="setSelectedTab('add-resources')" :mode="addResButtonMode">Add User</base-button>
        
    </base-card>
    <keep-alive>
         <component :is="selectedTab"></component>
    </keep-alive>
   
</template>

<script>

import BaseButton from '../UI/BaseButton.vue'
import StoredResources from './StoredResources';
import AddResources from './AddResource';
// import axios from 'axios';
import userJson from '../../../public/users.json'
import OrgJson from '../../../public/organizations.json'

export default {

components: { 
      BaseButton,
      StoredResources,
      AddResources 
},

 created: function() {
       this.storedResources = userJson;
          this.storedOrgResources = OrgJson;
        console.log(userJson);
 },

data(){
        return {
            selectedTab:'stored-resources',
            storedResources:userJson,
            storedOrgResources:OrgJson,
            searchQuery:null,
        }
    },
    methods:{
        
        setSelectedTab(tab){
            this.selectedTab = tab;
        },
      
        addResource(name,phone,url,email,signature,role,timezone){
            const newResource = {
                id:new Date().toISOString(),
                name:name,
                email:email,
                url:url,
                role:role,
                signature:signature,
                timezone:timezone,
            }
            this.storedResources.unshift(newResource);
            this.selectedTab = 'stored-resources';
        },

        removeResource(resId){

            const resIndex = this.storedResources.findIndex(
                (res) => res.id === resId
            )
            this.storedResources.splice(resIndex,1);

        },


    },
    provide(){
        return {
            $resources: () => this.resultQuery,
            addResource:this.addResource,
            deleteResource:this.removeResource,
            result:this.searchQuery
        }
    },
    computed:{
        storedResButtonMode(){
            return this.selectedTab === 'stored-resources' ? null : 'flat';
        },
        addResButtonMode(){
          return  this.selectedTab === 'add-resources' ? null : 'flat';
           
        },
        resultQuery(){
          
            if(this.searchQuery){
                   
                return this.storedResources.filter((item)=> {
                    return this.searchQuery.toLowerCase().split(' ').every(
                        v => item.name.toLowerCase().includes(v),
                      //  x => item.email.toLowerCase().includes(x),
                        )
                })
            }else{
                return this.storedResources;
            }
        }
       
    },
  
}
</script>
<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>

