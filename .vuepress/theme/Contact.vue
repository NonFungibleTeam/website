<template>
  <div class="base-layout">
    <Nav />
    <v-content>
      <v-container fluid>
        <v-layout class="pa-4 page-title" align="center">
          <h1>{{ $page.title }}</h1>
        </v-layout>
        <v-layout class="pa-4">
          <v-flex xs12 md10 offset-md1>
            <v-card class="contact-info pa-4 ma-4">
              <h1>{{ $page.frontmatter.contactBlurb }}</h1>
              <h2>
                Email:
                <a :href="'mailto:' + $page.frontmatter.email">{{ $page.frontmatter.email }}</a>
              </h2>
              <Content />
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
    </v-content>
  </div>
</template>
<script>
import Nav from "./components/Nav";
import axios from "axios";

export default {
  data: () => ({
    valid: true,
    alertType: "info",
    alert: "",
    name: "",
    nameRules: [v => !!v || "Name is required"],
    email: "",
    emailRules: [
      v => !!v || "E-mail is required",
      v => /.+@.+/.test(v) || "E-mail must be valid"
    ],
    subject: "",
    subjectRules: [v => !!v || "Subject is required"],
    message: "",
    messageRules: [v => !!v || "Message is required"]
  }),
  methods: {
    submit() {
      if (this.$refs.form.validate()) {
        let url = "/.netlify/functions/contact";
        axios
          .post(url, {
            name: this.name,
            email: this.email,
            subject: this.subject,
            message: this.message
          })
          .then(resp => {
            // check request result for success
            this.alert = "Message Sent!";
            this.alertType = "success";
            this.$refs.form.reset();
          })
          .catch(error => {
            this.alert = "An Error Ocurred!";
            this.alertType = "error";
            console.error(error);
          });
      }
    },
    clear() {
      this.$refs.form.reset();
    }
  },
  components: {
    Nav
  }
};
</script>
<style>
.card-header {
  text-align: center;
}
@media (max-width: 425px) {
  .contact-info {
    font-size: 0.9em;
  }
}
@media (max-width: 350px) {
  .contact-info {
    font-size: 0.75em;
  }
}
</style>
