<template>
    <Page class="body">
        <ActionBar>
            <Label text="Converter" class="header" />
        </ActionBar>
        <StackLayout>
            <Button text="Back" @tap="$navigateTo(TimePage)" class="button" style="margin-top: 30px;" />          
            <template v-if="reverseStatus" >
                <StackLayout>
                    <Label text="from week:" class="row-items"/>
                    <TextField v-model="week" class="row-items row-input-text input"/>
                    <Button text="<=>" @tap="reverse()" class="button"/>
                    <Label text="to year:" class="row-items"/>
                    <Label v-model="year" class="row-items row-input-text"/>
                </StackLayout>
                <Button text="Convert" @tap="convert()" class="button" />
            </template>
            <template v-else>
                <StackLayout>
                    <Label text="from year:" class="row-items"/>
                    <TextField v-model="year" class="row-items row-input-text input"/>
                    <Button text="<=>" @tap="reverse()" class="button"/>
                    <Label text="to week:" class="row-items"/>
                    <Label v-model="week" class="row-items row-input-text"/>
                </StackLayout>
                <Button text="Convert" @tap="convert()" class="button" />
            </template>
            <Keyboard class="keyboard"
                :firstValue="week"
                :secondValue="year"
                :reverseStatus="reverseStatus"
                @updateParents="update"
            />
        </StackLayout>
    </Page>
</template>

<script>
import timePage from './TimePage.vue'
import Keyboard from '../Keyboard.vue'
    export default {
    data() {
        return {
            week: '',
            year: '',
            weekYear: 52.1786,
            reverseStatus: true,
            TimePage: timePage,
        }
    },
    components: {Keyboard},
    methods: {
        reverse() {
            this.reverseStatus = !this.reverseStatus
            this.week = this.year = ''     
        },
        convert() {
            if (this.reverseStatus === false) {
                this.week = this.year*this.weekYear
                if (isNaN(this.week)) {
                    this.week = 'Error'
                }
            }
            if (this.reverseStatus === true) {
                this.year = this.week/this.weekYear
                if (isNaN(this.year)) {
                    this.year = 'Error'
                }
            } 
        },
        update(data) {
            this.week = data.first
            this.year = data.second
        }
    },
};
</script>

<style src="@/style-converter.css"></style>