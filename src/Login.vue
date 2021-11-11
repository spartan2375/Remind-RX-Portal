<template>
  <div>
    <div class="bg pa-6">
      <!-- <v-img src="login.jpg"> </v-img> -->
      <v-container class="pa-10">
        <v-row justify="center">
          <v-card dark>
            <v-card-title class="text-h3 ">
              RemindRX
            </v-card-title>
            <v-card-subtitle>
              A Better Life for Patients
            </v-card-subtitle>

            <v-divider></v-divider>
            <v-card-text>
              Please enter your credentials
              <v-text-field
                class="pt-3"
                dense
                outlined
                v-model="username"
                label="Username"
              >
              </v-text-field>
              <v-text-field
                dense
                outlined
                v-model="password"
                :append-icon="showPass ? 'mdi-eye' : 'mdi-eye-off'"
                :rules="[rules.required, rules.min]"
                :type="showPass ? 'text' : 'password'"
                label="Password"
                @click:append="showPass = !showPass"
              >
              </v-text-field>
            </v-card-text>
            <v-card-actions class="pa-6">
              <v-row justify="center">
                <v-btn @click.stop="$emit('log-me-in')" to="/Tasks"
                  >Login</v-btn
                >
              </v-row>
            </v-card-actions>
          </v-card>
        </v-row>
      </v-container>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showPass: false,
      username: "",
      password: "",
      rules: {
        required: (value) => !!value || "Required.",
        min: (v) => v.length >= 8 || "Min 8 characters",
        emailMatch: () => `The email and password you entered don't match`,
      },
      settings: [
        {
          title: "Keep me logged in",
          icon: "mdi-account-lock",
          color: "red",
        },
        {
          title: "Change password",
          icon: "mdi-lock-reset",
          color: "primary",
        },
      ],
    };
  },

  methods: {
    clickMe() {
      console.log("Click Me");
      this.dialog = false;
    },
  },
};
</script>
<style>
.bg {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  background: url("../public/login.jpg") no-repeat center center;
  background-size: cover;
  background-color: black;
  transform: scale(1);
}
/* html {
  background: url("../public/login.jpg") no-repeat center center fixed;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
} */
/* div[data-app="true"] {
  background: url("../public/login.jpg") no-repeat center center fixed !important;
  background-size: cover;
} */
</style>
