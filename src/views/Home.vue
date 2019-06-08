<template lang="pug">
  .home
    v-content
      v-container(fill-height="")
        v-layout(row="" justify-center="")
          h1 ニンニク入れますか
          .spell(v-if="spellActive")
            h2 呪文
            h2 {{spell}}
          div
            v-dialog(v-model="dialog" scrollable="" max-width="300px")
                template(v-slot:activator="{ on }")
                    v-btn(color="primary" dark="" v-on="on") Open Dialog
                v-card
                    v-card-title 呪文構成
                    div
                      v-tabs(v-model="active" color="cyan" dark="" slider-color="yellow")
                          v-tab(v-for=" topping in toppings" ripple="")
                              | {{topping.name}}
                          v-tab-item(v-for="topping in toppings")
                              v-card-text(style="height: 300px;")
                                  v-radio-group(v-model="topping.amount" column="")
                                      v-radio(v-for="amount in amounts" :label="amount.title" :value="amount.value")
                      .text-xs-center.mt-3
                          v-btn(@click="next") 次へ
                    v-divider
                    v-card-actions
                        v-btn(color="blue darken-1" flat="" @click="dialog = false") Close
                        v-btn(color="blue darken-1" flat="" @click="showSpell()") Save

</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
@Component({
  components: {}
})
export default class Home extends Vue {
  username: string = "";
  active: number = 0;
  spellActive = false;
  toppings: any = [
    {
      name: "ニンニク",
      amount: 0
    },
    {
      name: "ヤサイ",
      amount: 0
    },
    {
      name: "カラメ",
      amount: 0
    },
    {
      name: "アブラ",
      amount: 0
    }
  ];

  amounts: any = [
    {
      title: "なし",
      value: 0
    },
    {
      title: "多い",
      value: 1
    },
    {
      title: "とても多い",
      value: 2
    },
    {
      title: "フードファイター",
      value: "3"
    }
  ];

  amountSpells: any = ["なし", "", "マシ", "マシマシ"];

  dialog = false;

  props = {
    source: String
  };

  private next() {
    const active = this.active;
    this.active = active < 3 ? active + 1 : 0;
  }

  get spell(): any {
    if (this.toppings[0].amount == 0) {
    }
    return `${this.toppings[0].name}${
      this.amountSpells[this.toppings[0].amount]
    }`;
  }

  private showSpell() {
    this.dialog = false;
    this.spellActive = true;
  }
}
</script>
