<template lang="pug">
  .home
    v-content
      v-container()
        v-layout(align-center justify-center)
          .display-1.font-weight-regular ニンニク入れますか
        v-layout(align-center justify-center)
            v-dialog(v-model="dialog" scrollable="" max-width="300px")
                template(v-slot:activator="{ on }")
                    v-btn(color="primary" dark="" v-on="on") 呪文生成
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
                          v-btn(color="blue darken-1" flat="" @click="showSpell()") Save
        v-layout(align-center justify-center)
          .spell(v-if="spellActive")
            .font-weight-medium.headline {{spell}}
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
    let nin = "";
    let yasa = "";
    let kara = "";
    let abu = "";
    if (this.toppings[0].amount !== 5) {
      nin = `${this.toppings[0].name}${
        this.amountSpells[this.toppings[0].amount]
      }`;
    }
    if (this.toppings[1].amount !== 5) {
      yasa = `${this.toppings[1].name}${
        this.amountSpells[this.toppings[1].amount]
      }`;
    }
    if (this.toppings[2].amount !== 5) {
      kara = `${this.toppings[2].name}${
        this.amountSpells[this.toppings[2].amount]
      }`;
    }
    if (this.toppings[3].amount !== 5) {
      abu = `${this.toppings[3].name}${
        this.amountSpells[this.toppings[3].amount]
      }`;
    }
    let result = `${nin}${yasa}${abu}${kara}`;
    if (result == "") {
      result = "";
    }
    return `${nin}${yasa}${abu}${kara}`;
  }

  private showSpell() {
    this.dialog = false;
    this.spellActive = true;
  }
}
</script>
