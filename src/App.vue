<template>
  <div id="app">
    <v-app>
      <v-card>
        <v-card-title class="indigo white--text headline">User Directory</v-card-title>
        <v-layout justify-space-between pa-4>
          <!-- 左側ペイン -->
          <v-flex xs5>
            <v-treeview
              :active.sync="active"
              :open.sync="open"
              :items="items"
              activatable
              open-on-click
              transition
            >
              <template v-slot:prepend="{ item, open, active }">
                <v-icon v-if="!item.file">{{ open ? 'mdi-folder-open' : 'mdi-folder' }}</v-icon>
                <v-icon v-else>{{ files[item.file] }}</v-icon>
              </template>
            </v-treeview>
          </v-flex>

          <v-divider vertical></v-divider>

          <!-- 右側ペイン -->
          <v-flex d-flex text-center>
            <v-scroll-y-transition mode="out-in">
              <div
                v-if="!selected"
                class="title grey--text text--lighten-1 font-weight-light"
                style="align-self: center;"
              >Select a item</div>

              <v-card v-else :key="selected.id" class="pt-6 mx-auto" flat max-width="400">
                <v-card-text>
                  <v-img
                    src="https://www.ryutsuu.biz/images/2019/03/20190325plant.jpg"
                    class="mb-6"
                  ></v-img>
                  <h3 class="headline mb-2">{{ selected.name }}</h3>
                </v-card-text>
                <v-divider></v-divider>
                <v-layout tag="v-card-text" text-left warp>
                  <v-flex tag="strong" xs5 text-right mr-4 mb-2>type:</v-flex>
                  <v-flex>{{ selected.file }}</v-flex>
                </v-layout>
              </v-card>
            </v-scroll-y-transition>
          </v-flex>
        </v-layout>
      </v-card>
    </v-app>
  </div>
</template>

<script>
export default {
  data: () => ({
    open: [],
    files: {
      html: "mdi-language-html5",
      js: "mdi-nodejs",
      json: "mdi-json",
      md: "mdi-markdown",
      pdf: "mdi-file-pdf",
      png: "mdi-file-image",
      txt: "mdi-file-document-outline",
      xls: "mdi-file-excel"
    },
    active: [],
    items: [
      {
        id: 1,
        name: ".git"
      },
      {
        id: 2,
        name: "node_modules"
      },
      {
        id: 3,
        name: "public",
        children: [
          {
            id: 4,
            name: "static",
            children: [
              {
                id: 5,
                name: "logo.png",
                file: "png"
              }
            ]
          },
          {
            id: 6,
            name: "favicon.ico",
            file: "png"
          },
          {
            id: 7,
            name: "index.html",
            file: "html"
          }
        ]
      },
      {
        id: 8,
        name: ".gitignore",
        file: "txt"
      },
      {
        id: 9,
        name: "babel.config.js",
        file: "js"
      },
      {
        id: 10,
        name: "package.json",
        file: "json"
      },
      {
        id: 11,
        name: "README.md",
        file: "md"
      },
      {
        id: 12,
        name: "vue.config.js",
        file: "js"
      },
      {
        id: 22223,
        name: "yarn.lock",
        file: "txt"
      }
    ]
  }),
  computed: {
    selected() {
      if (!this.active.length) return undefined;

      const id = this.active[0];

      console.log(this.active);

      return this.items.find(item => item.id === id);
    }
  },

  watch: {}
};
</script>