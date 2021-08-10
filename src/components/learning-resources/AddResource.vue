<template>

    <base-dialog v-if="inputIsInvalid" title="Invalid Input" @close="confirmError">
        <template #default>
            <p>Unfortunately, atlean one input feild is invalid</p>
            <p>Please check the all the inputs and mak sure you enter at least one input</p>
        </template>
        <template #actions>
            <base-button @click="confirmError">Okay</base-button>
        </template>
    </base-dialog>

   <base-card>

    <form @submit.prevent="submitData">
            <div class="form-control">
                    <label for="name"> Name</label>
                    <input id="name" name="name" type="text" ref="nameInput" />
            </div>
             <div class="form-control">
                    <label for="phone">Phone</label>
                    <input id="phone" name="phone" type="text" ref="phoneInput" />
            </div>
            <div class="form-control">
                    <label for="email">Email</label>
                    <input id="email" name="email" type="text" ref="emailInput" />
            </div>
            <div class="form-control">
                    <label for="signature">Signature</label>
                    <input id="signature" name="signature" type="text" ref="signatureInput" />
            </div>

             <div class="form-control">
                    <label for="role">Role</label>
                    <input id="role" name="role" type="text" ref="roleInput" />
            </div>

             <div class="form-control">
                    <label for="timezon">timezon</label>
                    <input id="timezon" name="timezon" type="text" ref="timezoneInput" />
            </div>

          

            <div class="form-control">
                    <label for="link">link</label>
                    <input id="link" name="link" type="text" ref="linkInput"/>
            </div>
            <base-button type="submit" >Save</base-button>
    </form>
   </base-card>

</template>
<script>
export default {
    inject:['addResource'],
    data(){
        return {
            inputIsInvalid:false,
        }
    },
    methods:{
        submitData(){
            console.log('hi')
            const enteredName = this.$refs.nameInput.value;
            const enteredPhone = this.$refs.phoneInput.value;
            const enteredUrl = this.$refs.linkInput.value;

            const enteredEmail = this.$refs.emailInput.value;
            const enteredSignature = this.$refs.signatureInput.value;

            const enteredRole = this.$refs.roleInput.value;
            const enteredTimezone = this.$refs.timezoneInput.value;
            
            if(
                enteredName.trim() === '' || enteredPhone.trim() === '' || enteredUrl.trim() === '' 
                || enteredEmail.trim() === '' || enteredSignature.trim() === ''
            ){
                this.inputIsInvalid = true ;
                return;
            }
            this.addResource(enteredName,enteredPhone,enteredUrl,enteredEmail,enteredSignature,enteredRole,enteredTimezone);
        },
        confirmError(){
             console.log('by')
            this.inputIsInvalid = false;
        },
      
    }
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