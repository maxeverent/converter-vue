<template>
    <Page class="body">
        <ActionBar>
            <Label text="Converter" class="header" />
        </ActionBar>
        <StackLayout>
            <Button text="Back" @tap="$navigateTo(CurrencyPage)" class="button" style="margin-top: 30px;" />          
            <template v-if="reverseStatus" >
                <StackLayout>
                    <Label text="from Rub:" class="row-items"/>
                    <TextField v-model="Rub" class="row-items row-input-text input"/>
                    <Button text="<=>" @tap="reverse()" class="button"/>
                    <Label text="to Hrivnia:" class="row-items"/>
                    <Label v-model="Hrivnia" class="row-items row-input-text"/>
                </StackLayout>
                <Button text="Convert" @tap="convert()" class="button" />
            </template>
            <template v-else>
                <StackLayout>
                    <Label text="from Hrivnia:" class="row-items"/>
                    <TextField v-model="Hrivnia" class="row-items row-input-text input"/>
                    <Button text="<=>" @tap="reverse()" class="button"/>
                    <Label text="to Rub:" class="row-items"/>
                    <Label v-model="Rub" class="row-items row-input-text"/>
                </StackLayout>
                <Button text="Convert" @tap="convert()" class="button" />
            </template>
            <Keyboard class="keyboard"
                :firstValue="Rub"
                :secondValue="Hrivnia"
                :reverseStatus="reverseStatus"
                @updateParents="update"
            />
        </StackLayout>
    </Page>
</template>

<script>
import currencyPage from './CurrencyPage.vue'
import Keyboard from '../Keyboard.vue'
    export default {
    data() {
        return {
            Rub: '',
            Hrivnia: '',
            HrivniaRub: 0.59,
            reverseStatus: true,
            CurrencyPage: currencyPage,
        }
    },
    components: {Keyboard},
    methods: {
        reverse() {
            this.reverseStatus = !this.reverseStatus
            this.Rub = this.Hrivnia = ''     
        },
        convert() {
            if (this.reverseStatus === false) {
                this.Rub = this.Hrivnia/this.HrivniaRub
                if (isNaN(this.Rub)) {
                    this.Rub = 'Error'
                }
            }
            if (this.reverseStatus === true) {
                this.Hrivnia = this.Rub*this.HrivniaRub
                if (isNaN(this.Hrivnia)) {
                    this.Hrivnia = 'Error'
                }
            } 
        },
        update(data) {
            this.Rub = data.first
            this.Hrivnia = data.second
        }
    },
};
</script>

<style src="@/style.css"></style>