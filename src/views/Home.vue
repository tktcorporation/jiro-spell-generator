<template lang="pug">
  .home
    v-content
      v-container(fill-height="")
        v-layout(justify-center="" align-center="")
          v-flex(shrink="")
              h1 ニンニク入れますか
        v-layout(row="" justify-center="")
          v-dialog(v-model="dialog" scrollable="" max-width="300px")
              template(v-slot:activator="{ on }")
                  v-btn(color="primary" dark="" v-on="on") Open Dialog
              v-card
                  v-card-title Select Country
                  v-divider
                  div
                    v-tabs(v-model="active" color="cyan" dark="" slider-color="yellow")
                        v-tab(v-for="n in 3" :key="n" ripple="")
                            | Item {{ n }}
                        v-tab-item(v-for="n in 3" :key="n")
                            v-card-text(style="height: 300px;")
                                v-radio-group(v-model="dialogm1" column="")
                                    v-radio(label="Bahamas, The" value="bahamas")
                                    v-radio(label="Bahrain" value="bahrain")
                                    v-radio(label="Bangladesh" value="bangladesh")
                                    v-radio(label="Barbados" value="barbados")

                    .text-xs-center.mt-3
                        v-btn(@click="next") next tab
                  v-divider
                  v-card-actions
                      v-btn(color="blue darken-1" flat="" @click="dialog = false") Close
                      v-btn(color="blue darken-1" flat="" @click="dialog = false") Save

</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
@Component({
  components: {}
})
export default class Home extends Vue {
  username: string = "";
  drawer = true;
  active: number = 0;

  items = [
    { icon: "trending_up", text: "Most Popular" },
    { icon: "subscriptions", text: "Subscriptions" },
    { icon: "history", text: "History" },
    { icon: "featured_play_list", text: "Playlists" },
    { icon: "watch_later", text: "Watch Later" }
  ];
  items2 = [
    { picture: 28, text: "Joseph" },
    { picture: 38, text: "Apple" },
    { picture: 48, text: "Xbox Ahoy" },
    { picture: 58, text: "Nokia" },
    { picture: 78, text: "MKBHD" }
  ];
  props = {
    source: String
  };

  next() {
    const active = this.active;
    this.active = active < 2 ? active + 1 : 0;
  }
}
</script>
