<template>
    <div id="employee-form">
    <form @submit.prevent="handleSubmit">
    <label>Employee Name</label>
    <input v-model="employee.name"
      ref="first"
     @focus="clearStatus"
    :class="{'has-error':submitting && invalidName }"
    type="text"/>
    <label>Employee Email</label>
    <input v-model="employee.email" 
    :class="{'has-error':submitting && invalidName }"
    @focus="clearStatus"
    type="text"/>
    <p v-if="error && submitting" class="error-message">
       ❗Please fill out all required fields
     </p>
    <button>Add Employee</button>
    <p v-if="success" class="success-message">
      ✅ Employee successfully added
    </p>
       </form>  
    </div>
</template>

<script>
export default {
    name:'employee-form',
    data(){
        return{
         submitting:false,
         error: false,
         success: false,   
         employee:{
             name:'',
             email:'',
         },
       }
    },
    methods: {
      handleSubmit() {
         this.submitting=true
         this.clearStatus()
         
         if(this.inavalidName||this.inavalidEmail){
             this.error=true
             return
         }
         
        this.$emit('add:employee',this.employee) 
        this.success=true
      },
      clearStatus(){
          this.success=false
          this.error=false
      },
    },
    computed:{
       inavalidName(){
        return this.employee.name===''
       },
        inavalidEmail(){
        return this.employee.email===''
       },
    },
}
</script>

<style scoped>
  form {
    margin-bottom: 2rem;
  }

  [class*='-message'] {
    font-weight: 500;
  }

  .error-message {
    color: #d33c40;
  }

  .success-message {
    color: #32a95d;
  }
</style>