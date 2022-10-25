<template>
    <Page class="body">
        <ActionBar>
            <Label text="LengthPage" class="header" />
        </ActionBar>
        <StackLayout>
            <Button text="Back" @tap="$navigateTo(HomePage)" class="button-page" /> 
            <Button text ="Kilometer-foot" @tap="$navigateTo(KilFoot)" class="button-page button-length" />
            <Button text ="Foot-decimeter" @tap="$navigateTo(FootDec)" class="button-page button-length" />
        </StackLayout>
    </Page>
</template>

<script>
import kilFoot from './KilometrsFoots.vue'
import footDec from './FootDecimeter.vue'
import HomePage from '../Home.vue'
    export default {
        data() {
            return {
                KilFoot: kilFoot,
                FootDec: footDec,
                HomePage: HomePage,
            }
        }
    }
</script>

<style src="@/style.css"></style>