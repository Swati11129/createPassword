<template>
  <v-container class="" style="margin: auto; width: 540px">
    <div class=" text-left">
      <div class="font-weight-bold text-h5">Hello Roger George</div>
      <div class="mb-6">Create new password</div>

      <div class="mb-6 font-weight-bold d-flex" style="gap: 10px;">
        <div style="gap:3px">
            <v-icon color=""  > mdi-email </v-icon>
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
        <input type="password" v-model="password" @focus=" remove='' "  class="mb-2" />
      </div>
      <div>
        <label>Confirm Password</label>
        <br />
        <input type="password" v-model="confirmPassword" class="mb-3" />
      </div>
      <div v-if="strongPassword"  class="red--text mb-3" >{{ strongPassword }}</div>
      <v-btn  :disabled="true" class="" style="">Create</v-btn>
    </div>
  </v-container>
</template>
<script>
export default {
  name: "createPassword",
  data() {
    return {
      password: "",
      confirmPassword: "",
      warn:"show"
    };
  },
  methods:{
    removeWarnig(){
      this.remove="remove";
    }
  },
  computed: {
    strongPassword() {
      if(this.warn==""){
        return "";
      }
      if(this.password==""){
        return "Password must be there";
      }
      if (this.password.length < 8) {
        return "New Password must be at least 8 characters";
      }
      if (!(/[a-z]/.test(this.password))) {
        return "Password not strong. Add: ! @, 123, abc, ABC";
      }
      if (!(/[A-Z]/.test(this.password))) {
        return "Password not strong. Add: ! @, 123, abc, ABC";
      }
      if (!(/[0-9]/.test(this.password))) {
        return "Password not strong. Add: ! @, 123, abc, ABC";
      }
      if (!(/[@!]/.test(this.password))) {
        return "Password not strong. Add: ! @, 123, abc, ABC";
      }
      if(this.confirmPassword==""){
        return "Password must be there";
      }
      if(this.confirmPassword!="" && this.password!=this.confirmPassword){
        return "Password not matching"
      }
    },
  },
};
</script>
