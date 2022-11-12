<template>
    <Page class="body">
        <ActionBar>
            <Label text="TemperaturePage" class="header" />
        </ActionBar>
        <StackLayout>
            <Button text="Back" @tap="$navigateTo(HomePage)" class="button-page" /> 
            <Button text ="Celsius-Fahrenheit" @tap="$navigateTo(CelFahr)" class="button-page button-page-celfahr" />
            <Button text ="Celsius-Kelvin" @tap="$navigateTo(CelKelv)" class="button-page button-page-celkel" />
        </StackLayout>
    </Page>
</template>

<script>
import celFahr from './CelsFahren.vue'
import celKelv from './CelsKelv.vue'
import HomePage from '../Home.vue'
    export default {
        data() {
            return {
                CelFahr: celFahr,
                CelKelv: celKelv,          
                HomePage: HomePage,
            }
        }
    }
</script>

<style src="@/style-converter.css"></style>