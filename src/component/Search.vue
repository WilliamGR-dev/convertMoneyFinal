<template>
    <div id="container">
        <ion-item>
            <ion-label position="stacked">Amount</ion-label>
            <ion-input type="number" placeholder="EUR" v-model="convert.money"></ion-input>
        </ion-item>
        <ion-item>
            <ion-label>To</ion-label>
            <ion-select ok-text="Okay" cancel-text="Dismiss" v-model="convert.devise">
                <ion-select-option v-for="(country, key) in AllCountry" :key="key" :value="key" >{{country}}</ion-select-option>
            </ion-select>
        </ion-item>
        <ion-button @click="searchMoney" expand="block" class="md button button-block button-solid ion-activatable ion-focusable hydrated" :disabled="!convert.money || !convert.devise">Convert</ion-button>
    </div>
</template>

<script>
    import { IonLabel, IonInput, IonItem, IonSelect, IonSelectOption, IonButton } from '@ionic/vue';
    export default {
        data() {
            return {
                AllCountry: [],
                convert: {
                    money: "",
                    devise: "",
                }
            }
        },
        name: "Search",
        methods: {
            findAllCountry() {
                fetch(`http://data.fixer.io/api/symbols?access_key=${process.env.VUE_APP_API_KEY}`)
                    .then(res => res.json())
                    .then(data => {
                        this.AllCountry = data.symbols;
                        this.error = ""
                    })
            },
            searchMoney() {
                this.$emit('money', this.convert);
            }
        },
        mounted() {
            this.findAllCountry()
        },
        components: {
            IonSelectOption,
            IonButton,
            IonSelect,
            IonItem,
            IonInput,
            IonLabel
        }

    }
</script>

<style scoped>

</style>