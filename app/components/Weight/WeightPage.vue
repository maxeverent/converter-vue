<template>
    <Page class="body">
        <ActionBar>
            <Label text="WeightPage" class="header" />
        </ActionBar>
        <StackLayout>
            <Button text="Back" @tap="$navigateTo(HomePage)" class="button-page" /> 
            <Button text ="Kilogram-gram" @tap="$navigateTo(KilogramGrams)" class="button-page button-page-kggr" />
            <Button text ="Kilogram-ton" @tap="$navigateTo(KilogramsTons)" class="button-page button-page-kgt" />
        </StackLayout>
    </Page>
</template>

<script>
import kilogramGrams from '../Weight/KilogramsGrams.vue'
import kilogramsTons from '../Weight/KilogramsTons.vue'
import HomePage from '../Home.vue'
    export default {
        data() {
            return {
                KilogramGrams: kilogramGrams,
                KilogramsTons: kilogramsTons,
                HomePage: HomePage,
            }
        }
    }
</script>

<style src="@/style-converter.css"></style>