<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>💰 Currency converter</ion-title>
      </ion-toolbar>
    </ion-header>
    
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">💰 Currency converter</ion-title>
        </ion-toolbar>
      </ion-header>
      <Search @money="convertData"></Search>
      <Result :convertMoney="convertMoney" v-show ="display"></Result>
    </ion-content>
  </ion-page>
</template>

<script>
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar } from '@ionic/vue';
import { defineComponent } from 'vue';
import Result from "@/component/Result";
import Search from "@/component/Search";

export default defineComponent({
  name: 'Home',
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    Result,
    Search
  },
  data() {
    return {
      convertMoney: {
        money: "",
        devise: "",
      },
      display: false,
    }
  },
  methods: {
    convertData(value) {
      this.display = true;
      this.convertMoney.money = value.money;
      this.convertMoney.devise = value.devise;

    }
  }
});
</script>

<style scoped>
#container {
  text-align: center;
  
  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;
  
  color: #8c8c8c;
  
  margin: 0;
}

#container a {
  text-decoration: none;
}
</style>