<template>
    <Page class="body">
        <ActionBar>
            <Label text="Converter" class="header" />
        </ActionBar>
        <StackLayout>
            <Button text="Back" @tap="$navigateTo(TimePage)" class="button" style="margin-top: 30px;" />          
            <template v-if="reverseStatus" >
                <StackLayout>
                    <Label text="from hours:" class="row-items"/>
                    <TextField v-model="hours" class="row-items row-input-text input"/>
                    <Button text="<=>" @tap="reverse()" class="button"/>
                    <Label text="to week:" class="row-items"/>
                    <Label v-model="week" class="row-items row-input-text"/>
                </StackLayout>
                <Button text="Convert" @tap="convert()" class="button" />
            </template>
            <template v-else>
                <StackLayout>
                    <Label text="from week:" class="row-items"/>
                    <TextField v-model="week" class="row-items row-input-text input"/>
                    <Button text="<=>" @tap="reverse()" class="button"/>
                    <Label text="to hours:" class="row-items"/>
                    <Label v-model="hours" class="row-items row-input-text"/>
                </StackLayout>
                <Button text="Convert" @tap="convert()" class="button" />
            </template>
            <Keyboard class="keyboard"
                :firstValue="hours"
                :secondValue="week"
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
            hours: '',
            week: '',
            weekHours: 168,
            reverseStatus: true,
            TimePage: timePage,
        }
    },
    components: {Keyboard},
    methods: {
        reverse() {
            this.reverseStatus = !this.reverseStatus
            this.hours = this.week = ''     
        },
        convert() {
            if (this.reverseStatus === false) {
                this.hours = this.week*this.weekHours
                if (isNaN(this.hours)) {
                    this.hours = 'Error'
                }
            }
            if (this.reverseStatus === true) {
                this.week = this.hours/this.weekHours
                if (isNaN(this.week)) {
                    this.week = 'Error'
                }
            } 
        },
        update(data) {
            this.hours = data.first
            this.week = data.second
        }
    },
};
</script>

<style src="@/style.css"></style>