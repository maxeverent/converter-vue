<template>
    <Page class="body">
        <ActionBar>
            <Label text="Converter" class="header" />
        </ActionBar>
        <StackLayout>
            <Button text="Back" @tap="$navigateTo(CurrencyPage)" class="button" style="margin-top: 30px;" />          
            <template v-if="reverseStatus" >
                <StackLayout>
                    <Label text="from Hrivnia:" class="row-items"/>
                    <TextField v-model="Hrivnia" class="row-items row-input-text input"/>
                    <Button text="<=>" @tap="reverse()" class="button"/>
                    <Label text="to Tenge:" class="row-items"/>
                    <Label v-model="Tenge" class="row-items row-input-text"/>
                </StackLayout>
                <Button text="Convert" @tap="convert()" class="button" />
            </template>
            <template v-else>
                <StackLayout>
                    <Label text="from Tenge:" class="row-items"/>
                    <TextField v-model="Tenge" class="row-items row-input-text input"/>
                    <Button text="<=>" @tap="reverse()" class="button"/>
                    <Label text="to Hrivnia:" class="row-items"/>
                    <Label v-model="Hrivnia" class="row-items row-input-text"/>
                </StackLayout>
                <Button text="Convert" @tap="convert()" class="button" />
            </template>
            <Keyboard class="keyboard"
                :firstValue="Hrivnia"
                :secondValue="Tenge"
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
            Hrivnia: '',
            Tenge: '',
            TengeHrivnia: 0.078,
            reverseStatus: true,
            CurrencyPage: currencyPage,
        }
    },
    components: {Keyboard},
    methods: {
        reverse() {
            this.reverseStatus = !this.reverseStatus
            this.Hrivnia = this.Tenge = ''     
        },
        convert() {
            if (this.reverseStatus === false) {
                this.Hrivnia = this.Tenge*this.TengeHrivnia
                if (isNaN(this.Hrivnia)) {
                    this.Hrivnia = 'Error'
                }
            }
            if (this.reverseStatus === true) {
                this.Tenge = this.Hrivnia/this.TengeHrivnia
                if (isNaN(this.Tenge)) {
                    this.Tenge = 'Error'
                }
            } 
        },
        update(data) {
            this.Hrivnia = data.first
            this.Tenge = data.second
        }
    },
};
</script>

<style src="@/style.css"></style>