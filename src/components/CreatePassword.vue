<template>
  <div class="d-flex" style="height: 100vh">
    <img
      src="../assets/cloudnuro logo.png"
      style="position: absolute; top: 20px; left: 20px; width: 80px"
    />

    <v-container style="margin: auto; width: 540px" class="text-left">
      <v-form ref="form" v-model="valid" >
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
        <div>Create Password</div>
          <v-text-field
            dense="false"
            :type="show1 ? 'text' : 'password'"
            @click:append="show1 = !show1"
            :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
            outlined
            v-model="password"
            :rules="[rules.createPasswordRequired, rules.strongPassword]"
            color="red"
            @blur="validate"
            @focus="validate"
          />
      </div>
      <div>
        <div>Confirm Password</div>
          <v-text-field
            dense="false"
            :type="show2 ? 'text' : 'password'"
            @click:append="show2 = !show2"
            :append-icon="show2 ? 'mdi-eye' : 'mdi-eye-off'"
            outlined
            v-model="confirmPassword"
            :rules="[rules.confirmPasswordRequired, rules.matchPassword]"
            color="red"
          />
        </div>
        <div class="text-right">
          <v-btn @click="validate" :disabled="!valid">Create</v-btn>
        </div>
      </v-form>
    </v-container>
  </div>
</template>
<script>
export default {
  name: "createPassword",
  data() {
    return {
      show1: false,
      valid:true,
      show2: false,
      password: "",
      confirmPassword: "",
      rules: {
        createPasswordRequired: (v) =>v.length != 0 || "Password Required",
        minLength: (v) =>v.length >= 8 || "New Password must be at least 8 characters",
        strongPassword: (v) =>
         ( /[a-z]+/.test(v) && /[A-Z]+/.test(v) && /[0-9]+/.test(v) && /[@!]+/.test(v) )||
          "Password not strong. Add: ! @, 123, abc, ABC",
        confirmPasswordRequired: (v) =>v.length != 0 || "Password must be there",
        matchPassword: (v) => v=== this.password || "Password not matching"
      },
    };
  },
  methods: {
    validate () {
         this.$refs.form.validate()
      },

  },

};
</script>
