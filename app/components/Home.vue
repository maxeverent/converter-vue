<template>
    <Page class="body">
        <ActionBar>
            <Label text="Converter" class="header" />
        </ActionBar>
        <StackLayout>
            <Button text ="Weight" @tap="$navigateTo(WeightPage)" class="button-home-page button-home-page-weigth" />
            <Button text ="Length" @tap="goToLengthPage()" class="button-home-page button-home-page-length"/>
            <Button text ="Temperature" @tap="$navigateTo(TemperaturePage)" class="button-home-page button-home-page-temperature"/>
            <Button text ="Сurrency" @tap="$navigateTo(CurrencyPage)" class="button-home-page button-home-page-currency"/>
            <Button text ="Time" @tap="$navigateTo(TimePage)" class="button-home-page button-home-page-time"/>
        </StackLayout>
    </Page>
</template>

<script>
import lengthPage from '../components/Length/LengthPage.vue'
import weightPage from '../components/Weight/WeightPage.vue'
import temperaturePage from '../components/Temperature/TemperaturePage.vue'
import currencyPage from '../components/Currency/CurrencyPage.vue'
import timePage from '../components/Time/TimePage.vue'
    export default {
        data() {
            return {
                WeightPage: weightPage,
                TemperaturePage: temperaturePage, 
                CurrencyPage: currencyPage, 
                TimePage: timePage,             
            }
        },
        methods: {
            goToLengthPage() {
                this.$navigateTo(lengthPage);
            }
        }  
    };
</script>

<style src="@/style.css"></style>
