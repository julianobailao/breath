<template>
  <v-app light>
    <div class="login__background"></div>
    <div class="login__background--bottom"></div>

    <v-card class="login__card">
      <v-card-text class="pb-1" primary-title>
        <img src="public/uds-logo.png" height="20">
      </v-card-text>
      <v-card-text class="pt-0">
        <h3 class="headline mb-0 grey--text">Entrar</h3>
      </v-card-text>
      <v-card-actions>
        <v-btn flat class="orange--text">Share</v-btn>
        <v-btn flat class="orange--text">Explore</v-btn>
      </v-card-actions>
    </v-card>

  </v-app>
</template>

<style lang="stylus">
  @import './stylus/main'

  .login__background,
  .login__background--bottom
    position absolute
    right 0
    left 0

  .login__background
    top 0
    bottom 50%
    background $theme['primary']

  .login__background--bottom
    top 50%
    bottom 0
    background $grey['lighten-2']

  .login__card
    position absolute
    left 50%
    top 50%
    width 320px
    transform translate(-50%, -50%)
</style>
