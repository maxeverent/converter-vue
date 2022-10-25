<template>
    <Page class="body">
        <ActionBar>
            <Label text="Converter" class="header" />
        </ActionBar>
        <StackLayout>
            <Button text="Back" @tap="$navigateTo(WeightPage)" class="button" style="margin-top: 30px;" />          
            <template v-if="reverseStatus" >
                <StackLayout>
                    <Label text="from kilograms:" class="row-items"/>
                    <TextField v-model="kilograms" editable="false" class="row-items row-input-text input"/>
                    <Button text="<=>" @tap="reverse()" class="button"/>
                    <Label text="to grams:" class="row-items"/>
                    <Label v-model="grams" editable="false" class="row-items row-input-text"/>
                </StackLayout>
                <Button text="Convert" @tap="convert()" class="button" />
            </template>
            <template v-else>
                <StackLayout>
                    <Label text="from grams:" class="row-items"/>
                    <TextField v-model="grams" editable="false" class="row-items row-input-text input"/>
                    <Button text="<=>" @tap="reverse()" class="button"/>
                    <Label text="to kilograms:" class="row-items"/>
                    <Label v-model="kilograms" editable="false" class="row-items row-input-text"/>
                </StackLayout>
                <Button text="Convert" @tap="convert()" class="button" />
            </template>
            <Keyboard class="keyboard"
                :firstValue="kilograms"
                :secondValue="grams"
                :reverseStatus="reverseStatus"
                @updateParents="update"
            />
        </StackLayout>
    </Page>
</template>

<script>
import WeightPage from '../Weight/WeightPage.vue'
import Keyboard from '../Keyboard.vue'
    export default {
    data() {
        return {
            kilograms: '',
            grams: '',
            reverseStatus: true,
            WeightPage: WeightPage,
        }
    },
    components: {Keyboard},
    methods: {
        reverse() {
            this.reverseStatus = !this.reverseStatus
            this.kilograms = this.grams = ''     
        },
        convert() {
            if (this.reverseStatus === false) {
                this.kilograms = this.grams/1000
                if (isNaN(this.kilograms)) {
                    this.kilograms = 'Error'
                }
            }
            if (this.reverseStatus === true) {
                this.grams = this.kilograms*1000
                if (isNaN(this.grams)) {
                    this.grams = 'Error'
                }
            } 
        },
        update(data) {
            this.kilograms = data.first
            this.grams = data.second
        }
    },
};
</script>

<style src="@/style.css"></style>