<template>
  <div class="d-flex" style="height: 100vh;">
    
    <img
      src="../assets/cloudnuro logo.png"
      style="position: absolute; top: 20px; left: 20px; width: 80px"
    />

    <v-container style="margin: auto; width: 540px" class=" text-left">
        <div class="font-weight-bold text-h5">Hello Roger George</div>
        <div class="mb-6">Create new password</div>
        <div class="mb-6 font-weight-bold d-flex" style="gap: 10px">
          <div>
            <v-icon> mdi-email </v-icon>
          </div>
          <div>roger.george@cloudnuro.com</div>
        </div>
        <div class="mb-3">
          Create a strong password! Use a combination of alphabets, numbers,
          special symbols and minimum of 8 characters
        </div>
        <div>
          <label>Create Password</label>
          <br />
          <v-text-field
            dense="false"
            :type="show1 ? 'text' : 'password'"
            @click:append="show1 = !show1"
            :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
            outlined
            v-model="password"
            @focus="removeWarning"
            @blur="showWarningMethod"
            color="red"
            style="height: 50px"
          />
        </div>
        <div v-if="showCreateWarning" class="red--text">{{ createWarningText }}</div>
        <div>
          <label>Confirm Password</label>
          <br />
          <v-text-field
            dense="false"
            :type="show2 ? 'text' : 'password'"
            @click:append="show2 = !show2"
            :append-icon="show2 ? 'mdi-eye' : 'mdi-eye-off'"
            outlined
            v-model="confirmPassword"
            @focus="removeConfirmWarning"
            @blur="showConfirmWarningMethod"
            color="red"
            style="height: 50px"
          />
        </div>
        <div v-if="showConfirmWarning" class="red--text">
          {{ confirmWarningText }}
        </div>

        <div class="text-right">
          <v-btn :disabled="showConfirmWarning || showCreateWarning || password!==confirmPassword " >Create</v-btn>
        </div>
    </v-container>
  </div>
</template>
<script>
export default {
  name: "createPassword",
  data() {
    return {
      show1: false,
      show2: false,
      password: "",
      confirmPassword: "",
      createWarningText: "",
      confirmWarningText: "",
      showCreateWarning: false,
      showConfirmWarning: false,
    };
  },
  methods: {
   
    
    removeWarning() {
      this.showCreateWarning = false;
    },
    removeConfirmWarning() {
      this.showConfirmWarning = false;
    },
    showWarningMethod() {
      if (this.password.length === 0) {
        this.showCreateWarning=true;
        this.createWarningText = "Password Required";
      } else if (this.password.length < 8) {
        this.showCreateWarning = true;
        this.createWarningText = "New Password must be at least 8 characters";
      } else if (!/[a-z]/.test(this.password)) {
        this.showCreateWarning = true;
        this.createWarningText = "Password not strong. Add: ! @, 123, abc, ABC";
      } else if (!/[A-Z]/.test(this.password)) {
        this.showCreateWarning = true;
        this.createWarningText = "Password not strong. Add: ! @, 123, abc, ABC";
      } else if (!/[0-9]/.test(this.password)) {
        this.showCreateWarning = true;
        this.createWarningText = "Password not strong. Add: ! @, 123, abc, ABC";
      } else if (!/[@!]/.test(this.password)) {
        this.showCreateWarning = true;
        this.createWarningText = "Password not strong. Add: ! @, 123, abc, ABC";
      } else {
        this.showCreateWarning = false;
      }
    },
    showConfirmWarningMethod() {
      if (this.showCreateWarning == false) {
        if (this.confirmPassword == "") {
          this.showConfirmWarning = true;
          this.confirmWarningText = "Password must be there";
        } else if (this.password != this.confirmPassword) {
          this.showConfirmWarning = true;
          this.confirmWarningText = "Password not matching";
        } else {
          this.showConfirmWarning = false;
        }
      } 
      else {
        this.showConfirmWarning = false;
      }
    },
  },
};
</script>
