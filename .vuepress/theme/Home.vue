<template>
  <div class="base-layout home">
    <Nav class="hidden-md-and-up" />
    <v-content>
      <v-container fluid>
        <v-parallax :src="$page.frontmatter.parallaxImage">
          <div class="paralax-body">
            <h1 class="paralax-title">{{ $page.frontmatter.parallaxHeader }}</h1>
            <h3 class="paralax-content">{{ $page.frontmatter.parallaxContent }}</h3>
          </div>
        </v-parallax>
        <v-layout class="menu hidden-sm-and-down">
          <v-toolbar dense color="secondary">
            <v-toolbar-items>
              <v-btn flat v-for="page in menuPages" :key="page.text" :to="page.link">{{ page.text}}</v-btn>
            </v-toolbar-items>
          </v-toolbar>
        </v-layout>
        <v-layout class="pa-4 body" wrap>
          <v-flex xs12 md10 offset-md1 class="pa-4 cards">
            <v-card v-for="card in $page.frontmatter.cards" min-width="25%" max-width="25%" class="ma-4 pa-2 card">
              <v-icon v-if="card.icon" class="pa-3 card-icon" x-large>{{ card.icon }}</v-icon>
              <v-img v-elseif="card.img" :src="card.img" width="100%" />
              <v-card-title>{{ card.text }}</v-card-title>
              <v-card-actions>
                <v-btn v-if="card.link" :href="card.link" target="_blank" >{{ card.linkText }}</v-btn>
                <v-btn v-else-if="card.linkTo" :to="card.linkTo">{{ card.linkText }}</v-btn>
              </v-card-actions>
            </v-card>
          </v-flex>
          <v-flex xs12 md10 offset-md1>
            <Content />
          </v-flex>
        </v-layout>
      </v-container>
    </v-content>
  </div>
</template>
<script>
import Nav from "./components/Nav";
export default {
  data: function() {
    return {};
  },
  computed: {
    menuPages() {
      let pages = this.$site.themeConfig.nav || [];
      return pages.filter(p => p.title !== "home");
    }
  },
  components: {
    Nav
  }
};
</script>
<style>
.container {
  padding: 0 !important;
}
.paralax-body {
  text-align: center;
  display: flex;
  align-items: center;
  flex-direction: column;
  text-shadow: 2px 2px 10px black;
}
.paralax-title {
  font-size: 3em;
}
.paralax-content {
  font-size: 1.8em;
}
.menu .v-btn {
  color: #fff !important;
}
.heading {
  display: flex;
}
.logo {
  margin: 10px;
  width: 300px;
  align-items: center;
}
.quote-block {
  padding-left: 1em;
  margin-top: 6%;
}
.quote-text {
  font-size: 2em;
}
.quote-avatar .v-image {
  transform: rotate(-90deg);
}
.quote-attr {
  display: flex;
}
.quote-attr-text {
  display: flex;
  flex-direction: column;
  padding-left: 1em;
  padding-top: 0.5em;
}
.body {
  display: flex;
  align-items: center;
}
.cards {
  margin: 10vh 0;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
}
.card {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  flex: 1;
}
.v-card__title {
  flex: 1 1 auto;
}
@media (max-width: 750px) {
  .heading {
    flex-direction: column;
  }
  .logo {
    width: 100%;
  }
  .card {
    flex: 100%;
  }
}
.text {
  margin: 10px;
  display: flex;
  align-items: center;
  flex-direction: column;
}
.home main {
  padding: 0 !important;
}
</style>
