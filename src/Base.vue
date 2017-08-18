<template>
  <v-app light>
    <v-navigation-drawer
      persistent
      :mini-variant="miniVariant"
      :clipped="clipped"
      v-model="drawer"
    >
      <v-toolbar dark class="primary white--text">
        <v-toolbar-title v-text="title"></v-toolbar-title>
      </v-toolbar>
      <div class="user-block">
        <div class="cover">
          <img src="public/polygon-mountain.jpg">
        </div>
      </div>
      <v-list>
        <v-list-tile
          v-for="(item, i) in menus"
          :key="i"
          value="true"
        >
          <v-list-tile-action>
            <v-icon light v-html="item.icon"></v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title v-text="item.title"></v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar fixed dark class="primary white--text" extended>
      <v-toolbar-title slot="extension">
        <div class="toolbar__extension__title">Dashboard</div>
        <div class="toolbar__extension__subtitle">Manage your dashboard data</div>
      </v-toolbar-title>
      <v-toolbar-side-icon @click.native.stop="drawer = !drawer"></v-toolbar-side-icon>
      <v-btn
        icon
        @click.native.stop="miniVariant = !miniVariant"
      >
        <v-icon v-html="miniVariant ? 'chevron_right' : 'chevron_left'"></v-icon>
      </v-btn>
      <v-btn
        icon
        @click.native.stop="clipped = !clipped"
      >
        <v-icon>web</v-icon>
      </v-btn>
      <v-btn
        icon
        @click.native.stop="fixed = !fixed"
      >
        <v-icon>remove</v-icon>
      </v-btn>
      <v-spacer></v-spacer>
      <v-btn
        icon
        @click.native.stop="rightDrawer = !rightDrawer"
      >
        <v-icon>menu</v-icon>
      </v-btn>
    </v-toolbar>
    <main>
      <v-container fluid>
        <v-slide-y-transition mode="out-in">
          <v-card class="card--flex-toolbar card--prominent">
            <v-toolbar card class="white">
              <v-toolbar-items>
                <v-btn flat class="grey--text">Link One</v-btn>
                <v-icon>chevron_right</v-icon>
                <v-btn flat class="grey--text">Link Two</v-btn>
                <v-icon>chevron_right</v-icon>
              </v-toolbar-items>
              <v-toolbar-title>Link Three</v-toolbar-title>
              <v-spacer></v-spacer>
              <v-btn icon>
                <v-icon>search</v-icon>
              </v-btn>
              <v-btn icon>
                <v-icon>apps</v-icon>
              </v-btn>
              <v-btn icon>
                <v-icon>more_vert</v-icon>
              </v-btn>
            </v-toolbar>
            <v-divider></v-divider>

            <v-data-table
              v-bind:headers="headers"
              v-bind:items="items"
              v-bind:search="search"
            >
            <template slot="items" scope="props">
              <td>
                <v-edit-dialog
                  @open="props.item._name = props.item.name"
                  @cancel="props.item.name = props.item._name || props.item.name"
                  lazy
                > {{ props.item.name }}
                  <v-text-field
                    slot="input"
                    label="Edit"
                    v-bind:value="props.item.name"
                    v-on:change="e => props.item.name = e.target.value"
                    single-line counter="counter"
                  ></v-text-field>
                </v-edit-dialog>
              </td>
              <td class="text-xs-right">{{ props.item.calories }}</td>
              <td class="text-xs-right">{{ props.item.fat }}</td>
              <td class="text-xs-right">{{ props.item.carbs }}</td>
              <td class="text-xs-right">{{ props.item.protein }}</td>
              <td class="text-xs-right">{{ props.item.sodium }}</td>
              <td class="text-xs-right">{{ props.item.calcium }}</td>
              <td class="text-xs-right">
                <v-edit-dialog
                  @open="props.item._iron = props.item.iron"
                  @cancel="props.item.iron = props.item._iron || props.item.iron"
                  large
                  lazy
                >
                  <div>{{ props.item.iron }}</div>
                  <div slot="input" class="mt-3 title">Update Iron</div>
                  <v-text-field
                    slot="input"
                    label="Edit"
                    v-model="props.item.iron"
                    single-line
                    counter
                    autofocus
                  ></v-text-field>
                </v-edit-dialog>
              </td>
            </template>
            <template slot="pageText" scope="{ pageStart, pageStop }">
              From {{ pageStart }} to {{ pageStop }}
            </template>
          </v-data-table>
          </v-card>
        </v-slide-y-transition>
      </v-container>
    </main>
    <v-navigation-drawer
      temporary
      :right="right"
      v-model="rightDrawer"
    >
      <v-list>
        <v-list-tile @click.native="right = !right">
          <v-list-tile-action>
            <v-icon light>compare_arrows</v-icon>
          </v-list-tile-action>
          <v-list-tile-title>Switch drawer (click me)</v-list-tile-title>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <v-footer :fixed="fixed">
      <span>&copy; 2017</span>
    </v-footer>
  </v-app>
</template>

<script>
  export default {
    data () {
      return {
        dark: true,
        clipped: false,
        drawer: true,
        fixed: false,
        menus: [
          { icon: 'bubble_chart', title: 'Inspire' }
        ],
        miniVariant: false,
        right: true,
        rightDrawer: false,
        title: 'Vuetify.js',
        search: '',
        pagination: {},
        headers: [
          {
            text: 'Dessert (100g serving)',
            align: 'left',
            sortable: false,
            value: 'name'
          },
          { text: 'Calories', value: 'calories' },
          { text: 'Fat (g)', value: 'fat' },
          { text: 'Carbs (g)', value: 'carbs' },
          { text: 'Protein (g)', value: 'protein' },
          { text: 'Sodium (mg)', value: 'sodium' },
          { text: 'Calcium (%)', value: 'calcium' },
          { text: 'Iron (%)', value: 'iron' }
        ],
        items: [
          {
            value: false,
            name: 'Frozen Yogurt',
            calories: 159,
            fat: 6.0,
            carbs: 24,
            protein: 4.0,
            sodium: 87,
            calcium: '14%',
            iron: '1%'
          },
          {
            value: false,
            name: 'Ice cream sandwich',
            calories: 237,
            fat: 9.0,
            carbs: 37,
            protein: 4.3,
            sodium: 129,
            calcium: '8%',
            iron: '1%'
          },
          {
            value: false,
            name: 'Eclair',
            calories: 262,
            fat: 16.0,
            carbs: 23,
            protein: 6.0,
            sodium: 337,
            calcium: '6%',
            iron: '7%'
          },
          {
            value: false,
            name: 'Cupcake',
            calories: 305,
            fat: 3.7,
            carbs: 67,
            protein: 4.3,
            sodium: 413,
            calcium: '3%',
            iron: '8%'
          },
          {
            value: false,
            name: 'Gingerbread',
            calories: 356,
            fat: 16.0,
            carbs: 49,
            protein: 3.9,
            sodium: 327,
            calcium: '7%',
            iron: '16%'
          },
          {
            value: false,
            name: 'Jelly bean',
            calories: 375,
            fat: 0.0,
            carbs: 94,
            protein: 0.0,
            sodium: 50,
            calcium: '0%',
            iron: '0%'
          },
          {
            value: false,
            name: 'Lollipop',
            calories: 392,
            fat: 0.2,
            carbs: 98,
            protein: 0,
            sodium: 38,
            calcium: '0%',
            iron: '2%'
          },
          {
            value: false,
            name: 'Honeycomb',
            calories: 408,
            fat: 3.2,
            carbs: 87,
            protein: 6.5,
            sodium: 562,
            calcium: '0%',
            iron: '45%'
          },
          {
            value: false,
            name: 'Donut',
            calories: 452,
            fat: 25.0,
            carbs: 51,
            protein: 4.9,
            sodium: 326,
            calcium: '2%',
            iron: '22%'
          },
          {
            value: false,
            name: 'KitKat',
            calories: 518,
            fat: 26.0,
            carbs: 65,
            protein: 7,
            sodium: 54,
            calcium: '12%',
            iron: '6%'
          }
        ]
      }
    }
  }
</script>

<style lang="stylus">
  @import './stylus/main'

  html, body, .application, .container
    overflow auto

  .toolbar--fixed.toolbar--extended + main
    padding-top 122px

    .container
      min-height calc(100vh - 159px)

  .card--prominent
    position relative
    z-index 3

  .user-block
    position relative
    z-index -1
    display block
    height 139px
    overflow hidden

    .cover
      position absolute
      top 0
      right 0
      bottom 0
      left 0
      animation pulse 30s infinite

      &:after
        content ''
        position absolute
        top 0
        right 0
        bottom 0
        left 0
        background linear-gradient(transparent, rgba(0,0,0,.6))

      img
        width 100%
        background-size cover

    @keyframes pulse
      0%
        transform scale(1.2)

      50%
        transform scale(1)

      100%
        transform scale(1.2)
</style>
