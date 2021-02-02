<template>
    <div>
        <h1>Resultat: </h1>
        <ion-card class="md hydrated">
            <ion-card-header class="ion-inherit-color md hydrated">
                <ion-card-subtitle class="ion-inherit-color md hydrated" role="heading" aria-level="3">{{Information.money}} EUR</ion-card-subtitle>
                <ion-card-title class="ion-inherit-color md hydrated" role="heading" aria-level="2">{{Information.moneyConverted}} {{Information.devise}}</ion-card-title>
            </ion-card-header>
        </ion-card>
    </div>
</template>

<script>
    import { IonCard, IonCardHeader, IonCardSubtitle, IonCardTitle } from '@ionic/vue';
    export default {
        props: ['convertMoney'],
        name: "Result",
        data() {
            return {
                Information: {
                    money: "",
                    devise: "",
                    moneyConverted: "",
                }
            }
        },
        watch: {
            convertMoney: {
                deep: true,
                handler(){
                    this.convert();
                }
            }
        },
        methods: {
            convert() {
                fetch(`http://data.fixer.io/api/latest?access_key=${process.env.VUE_APP_API_KEY}`)
                    .then(res => res.json())
                    .then(data => {
                        this.Information.devise = this.convertMoney.devise;
                        this.Information.money = this.convertMoney.money;
                        this.Information.moneyConverted =  Math.round((data.rates[this.Information.devise] * this.Information.money) * 100) / 100;
                    })
            }
        },
        components:{
            IonCard,
            IonCardTitle,
            IonCardSubtitle,
            IonCardHeader
        }
    }
</script>

<style scoped>

</style>