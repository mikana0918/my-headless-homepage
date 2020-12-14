<template>
  <div>
    <!-- ヘッダ -->
    <v-card>
      <v-toolbar
        color="deep-purple accent-4"
        dark
        flat
      >
        <v-app-bar-nav-icon></v-app-bar-nav-icon>

        <v-toolbar-title>Page title</v-toolbar-title>

        <v-spacer></v-spacer>

        <v-btn icon>
          <v-icon>mdi-magnify</v-icon>
        </v-btn>

        <v-btn icon>
          <v-icon>mdi-dots-vertical</v-icon>
        </v-btn>

        <template v-slot:extension>
          <v-tabs
            v-model="currentItem"
            fixed-tabs
            slider-color="white"
          >
            <v-tab
              v-for="item in items"
              :key="item"
              :href="'#tab-' + item"
            >
              {{ item }}
            </v-tab>

            <v-menu
              v-if="more.length"
              bottom
              left
            >
              <template v-slot:activator="{ on, attrs }">
                <v-btn
                  text
                  class="align-self-center mr-4"
                  v-bind="attrs"
                  v-on="on"
                >
                  more
                  <v-icon right>
                    mdi-menu-down
                  </v-icon>
                </v-btn>
              </template>

              <v-list class="grey lighten-3">
                <v-list-item
                  v-for="item in more"
                  :key="item"
                  @click="addItem(item)"
                >
                  {{ item }}
                </v-list-item>
              </v-list>
            </v-menu>
          </v-tabs>
        </template>
      </v-toolbar>

      <v-tabs-items v-model="currentItem">
        <v-tab-item
          v-for="item in items.concat(more)"
          :key="item"
          :value="'tab-' + item"
        >
          <v-card flat>
            <v-card-text>
              <h2>{{ item }}</h2>
              {{ text }}
            </v-card-text>
          </v-card>
        </v-tab-item>
      </v-tabs-items>
    </v-card>
    <!-- ページコンテンツ -->
    <Nuxt />
    <!-- フッタ -->
    <v-footer
        dark
        padless
        class="defaultFooter"
    >
      <v-card
      flat
      tile
      class="indigo lighten-1 white--text text-center"
      >
        <v-card-text>
            <v-btn
            v-for="icon in icons"
            :key="icon"
            class="mx-4 white--text"
            icon
            >
            <v-icon size="24px">
                {{ icon }}
            </v-icon>
            </v-btn>
        </v-card-text>
        <v-card-text class="white--text pt-0">
            Phasellus feugiat arcu sapien, et iaculis ipsum elementum sit amet. Mauris cursus commodo interdum. Praesent ut risus eget metus luctus accumsan id ultrices nunc. Sed at orci sed massa consectetur dignissim a sit amet dui. Duis commodo vitae velit et faucibus. Morbi vehicula lacinia malesuada. Nulla placerat augue vel ipsum ultrices, cursus iaculis dui sollicitudin. Vestibulum eu ipsum vel diam elementum tempor vel ut orci. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus.
        </v-card-text>
        <v-divider></v-divider>
        <v-card-text class="white--text">
            {{ new Date().getFullYear() }} — <strong>Shogo Kusuhara</strong>
        </v-card-text>
      </v-card>
    </v-footer>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'

@Component
export default class DefaultLayout extends Vue {
  icon: object =  {}
  currentItem: String = 'tab-Web'
  items: Array<String> = [
      'Web', 'Shopping', 'Videos', 'Images',
  ]
  more: Array<String> = [
    'News', 'Maps', 'Books', 'Flights', 'Apps',
  ]
  text: String = 'Lorem ipsum dolor sit amet,consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.'

  addItem (item: String) {
    const removed = this.items.splice(0, 1)
    this.items.push(
      ...this.more.splice(this.more.indexOf(item), 1),
    )
    this.more.push(...removed)
    this.$nextTick(() => { this.currentItem = 'tab-' + item })
  }
}
</script>

<style scoped lang="scss">
.defaultFooter {
  position: absolute;
  bottom: 0;
}
</style>
