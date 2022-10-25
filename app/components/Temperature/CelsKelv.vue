<template>
    <Page class="body">
        <ActionBar>
            <Label text="Converter" class="header" />
        </ActionBar>
        <StackLayout>
            <Button text="Back" @tap="$navigateTo(TemperaturePage)" class="button" style="margin-top: 30px;" />          
            <template v-if="reverseStatus" >
                <StackLayout>
                    <Label text="from Celsius:" class="row-items"/>
                    <TextField v-model="Celsius" class="row-items row-input-text input"/>
                    <Button text="<=>" @tap="reverse()" class="button"/>
                    <Label text="to Celvin:" class="row-items"/>
                    <Label v-model="Celvin" class="row-items row-input-text"/>
                </StackLayout>
                <Button text="Convert" @tap="convert()" class="button" />
            </template>
            <template v-else>
                <StackLayout>
                    <Label text="from Celvin:" class="row-items"/>
                    <TextField v-model="Celvin" class="row-items row-input-text input"/>
                    <Button text="<=>" @tap="reverse()" class="button"/>
                    <Label text="to Celsius:" class="row-items"/>
                    <Label v-model="Celsius" class="row-items row-input-text"/>
                </StackLayout>
                <Button text="Convert" @tap="convert()" class="button" />
            </template>
            <Keyboard class="keyboard"
                :firstValue="Celsius"
                :secondValue="Celvin"
                :reverseStatus="reverseStatus"
                @updateParents="update"
            />
        </StackLayout>
    </Page>
</template>

<script>
import temperaturePage from './TemperaturePage.vue'
import Keyboard from '../Keyboard.vue'
    export default {
    data() {
        return {
            Celsius: '',
            Celvin: '',
            CelvinCelsius: 274.15,
            reverseStatus: true,
            TemperaturePage: temperaturePage,
        }
    },
    components: {Keyboard},
    methods: {
        reverse() {
            this.reverseStatus = !this.reverseStatus
            this.Celsius = this.Celvin = ''     
        },
        convert() {
            if (this.reverseStatus === false) {
                this.Celsius = this.Celvin/this.CelvinCelsius
                if (isNaN(this.Celsius)) {
                    this.Celsius = 'Error'
                }
            }
            if (this.reverseStatus === true) {
                this.Celvin = this.Celsius*this.CelvinCelsius
                if (isNaN(this.Celvin)) {
                    this.Celvin = 'Error'
                }
            } 
        },
        update(data) {
            this.Celsius = data.first
            this.Celvin = data.second
        }
    },
};
</script>

<style src="@/style.css"></style>