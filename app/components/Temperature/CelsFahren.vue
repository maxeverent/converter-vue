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
                    <Label text="to Fahrenheit:" class="row-items"/>
                    <Label v-model="Fahrenheit" class="row-items row-input-text"/>
                </StackLayout>
                <Button text="Convert" @tap="convert()" class="button" />
            </template>
            <template v-else>
                <StackLayout>
                    <Label text="from Fahrenheit:" class="row-items"/>
                    <TextField v-model="Fahrenheit" class="row-items row-input-text input"/>
                    <Button text="<=>" @tap="reverse()" class="button"/>
                    <Label text="to Celsius:" class="row-items"/>
                    <Label v-model="Celsius" class="row-items row-input-text"/>
                </StackLayout>
                <Button text="Convert" @tap="convert()" class="button" />
            </template>
            <Keyboard class="keyboard"
                :firstValue="Celsius"
                :secondValue="Fahrenheit"
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
            Fahrenheit: '',
            FahrenheitCelsius: 33.8,
            reverseStatus: true,
            TemperaturePage: temperaturePage,
        }
    },
    components: {Keyboard},
    methods: {
        reverse() {
            this.reverseStatus = !this.reverseStatus
            this.Celsius = this.Fahrenheit = ''     
        },
        convert() {
            if (this.reverseStatus === false) {
                this.Celsius = this.Fahrenheit/this.FahrenheitCelsius
                if (isNaN(this.Celsius)) {
                    this.Celsius = 'Error'
                }
            }
            if (this.reverseStatus === true) {
                this.Fahrenheit = this.Celsius*this.FahrenheitCelsius
                if (isNaN(this.Fahrenheit)) {
                    this.Fahrenheit = 'Error'
                }
            } 
        },
        update(data) {
            this.Celsius = data.first
            this.Fahrenheit = data.second
        }
    },
};
</script>

<style src="@/style-converter.css"></style>