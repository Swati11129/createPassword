<template>
  <div class="d-flex" style="height:100vh;">

    <div>
      <img src="../assets/cloudnuro logo.png" style="position:absolute; top:20px; left:20px; width:80px"/>
    </div>
  
  <v-container class="" style="margin: auto; width: 540px">
    <div class=" text-left">
      <div class="font-weight-bold text-h5">Hello Roger George</div>
      <div class="mb-6">Create new password</div>

      <div class="mb-6 font-weight-bold d-flex" style="gap: 10px;">
        <div >
            <v-icon> mdi-email </v-icon>
        </div>
        <div >
            roger.george@cloudnuro.com
        </div>
      </div>
      <div class="mb-3">
        Create a strong password! Use a combination of alphabets, numbers,
        special symbols and minimum of 8 characters
      </div>
      <div>
        <label>Create Password</label>
        <br />
        <input type="password" v-model="password" @focus="removeWarning" @blur="showWarningMethod" class="mb-2" />
      </div>
      <div>
        <label>Confirm Password</label>
        <br />
        <input type="password" v-model="confirmPassword" @focus="removeConfirmWarning" @blur="showConfirmWarningMethod" class="mb-3" />
      </div>
      <div v-if="showWarning"  class="red--text mb-3" >{{ warningText }}</div>
      <div v-else-if="showConfirm" class="red--text mb-3" >{{ confirmWarningText }}</div>
      
      <div class="text-right ">
        <v-btn  :disabled="showConfirm || showWarning" >Create</v-btn>
      </div>
    </div>
  </v-container>
</div>
</template>
<script>
export default {
  name: "createPassword",
  data() {
    return {
      password: "",
      confirmPassword: "",
      warningText:"",
      confirmWarningText:"",
      showWarning:true,
      showConfirm:false,
    };
  },
  methods:{
    removeWarning(){
      this.showWarning=false;
    },
    removeConfirmWarning(){
      this.showConfirm=false;
    },
    showWarningMethod(){
      if(this.password.length==0){
        this.showWarning=true;
        this.warningText="Password required";
      }
      else if (this.password.length < 8) {
        this.showWarning=true;
        this.warningText='New Password must be at least 8 characters';
      }
      else if (!(/[a-z]/.test(this.password))) {
        this.showWarning=true;
        this.warningText= "Password not strong. Add: ! @, 123, abc, ABC";
      }
      else if (!(/[A-Z]/.test(this.password))) {
        this.showWarning=true;
        this.warningText= "Password not strong. Add: ! @, 123, abc, ABC";
      }
      else if (!(/[0-9]/.test(this.password))) {
        this.showWarning=true;
        this.warningText= "Password not strong. Add: ! @, 123, abc, ABC";
      }
      else if (!(/[@!]/.test(this.password))) {
        this.showWarning=true;
        this.warningText= "Password not strong. Add: ! @, 123, abc, ABC";
      }
      else{
        this.showWarning=false;
      }
    },
    showConfirmWarningMethod(){
      if(this.showWarning==false)
      {
       if(this.confirmPassword==""){
        this.showConfirm=true;
        this.confirmWarningText= "Password must be there";
      }
      else if( this.password!=this.confirmPassword){
        this.showConfirm=true;
        this.confirmWarningText= "Password not matching"
      }
      else{
        this.showConfirm=false;
      }
    }
    else{
      this.showConfirm=false;
    }
      
    }

  },

};
</script>
