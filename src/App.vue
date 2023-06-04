<template>
  <v-app>
    <v-app-bar app dark>
      <v-img alt="Vuetify Logo" class="shrink mx-auto" contain src="./assets/LOGO50A COR.png"
        transition="scale-transition" width="100" />

    </v-app-bar>

    <v-main>
      <div class="pl-10 pr-10 pt-10 pb-10">
        <router-view />
      </div>
    </v-main>

    <v-footer paddless dark class="d-flex justify-space-between">
      <v-card>
        <v-card-text class="white--text text-center">
          <strong>Docente:</strong> Adenilso da Silva Simão (<strong>adenilso@icmc.usp.br</strong>)
        </v-card-text>
      </v-card>

      <v-card flat tile class="white--text">

        <v-card-text class="white--text pt-0 text-center">
          SSC0961 - Desenvolvimento Web e Mobile
        </v-card-text>

        <v-divider></v-divider>

        <v-card-text class="white--text pt-0  pb-0 text-center">
          {{ new Date().getFullYear() }}
        </v-card-text>

      </v-card>

      <v-card>
        <v-card-text class="white--text text-center">
          <strong>Estagiário PAE:</strong> Rodrigo Henrique Ramos (<strong>rodrigohenrique.ramos@usp.br</strong>)
        </v-card-text>
      </v-card>
    </v-footer>
  </v-app>
</template>

<script>

export default {
  name: 'App',

  data: () => ({
    //
  })
}
</script>
