<template>
    <Page class="body">
        <ActionBar>
            <Label text="TimePage" class="header" />
        </ActionBar>
        <StackLayout>
            <Button text="Back" @tap="$navigateTo(HomePage)" class="button-page" /> 
            <Button text ="Hour-Week" @tap="$navigateTo(HourWeek)" class="button-page button-page-hourweek" />
            <Button text ="Week-Year" @tap="$navigateTo(WeekYear)" class="button-page button-page-weekyear" />
        </StackLayout>
    </Page>
</template>

<script>
import hourWeek from './HourWeek.vue'
import weekYear from './WeekYear.vue'
import HomePage from '../Home.vue'
    export default {
        data() {
            return {
                HourWeek: hourWeek, 
                WeekYear: weekYear,  
                HomePage: HomePage,
            }
        }
    }
</script>

<style src="@/style.css"></style>