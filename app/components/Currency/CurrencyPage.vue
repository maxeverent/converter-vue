<template>
    <Page class="body">
        <ActionBar>
            <Label text="LengthPage" class="header" />
        </ActionBar>
        <StackLayout>
            <Button text="Back" @tap="$navigateTo(HomePage)" class="button-page" /> 
            <Button text ="Rub-Hryvnia" @tap="$navigateTo(RubHr)" class="button-page button-page-rubhr" />
            <Button text ="Hryvnia-Tenge" @tap="$navigateTo(HrTenge)" class="button-page button-page-hrtenge" />
        </StackLayout>
    </Page>
</template>

<script>
import rubHr from './RubHryvnia.vue'
import hrTenge from './HryvniaTenge.vue'
import HomePage from '../Home.vue'
    export default {
        data() {
            return {
                RubHr: rubHr,
                HrTenge: hrTenge,
                HomePage: HomePage,
            }
        }
    }
</script>

<style src="@/style.css"></style>