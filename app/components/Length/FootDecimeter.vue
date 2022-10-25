<template>
    <Page class="body">
        <ActionBar>
            <Label text="Converter" class="header" />
        </ActionBar>
        <StackLayout>
            <Button text="Back" @tap="$navigateTo(lengthPage)" class="button" style="margin-top: 30px;" />          
            <template v-if="reverseStatus" >
                <StackLayout>
                    <Label text="from foots:" class="row-items"/>
                    <TextField v-model="foots" class="row-items row-input-text input"/>
                    <Button text="<=>" @tap="reverse()" class="button"/>
                    <Label text="to decumeters:" class="row-items"/>
                    <Label v-model="decimeters" class="row-items row-input-text"/>
                </StackLayout>
                <Button text="Convert" @tap="convert()" class="button" />
            </template>
            <template v-else>
                <StackLayout>
                    <Label text="from decumeters:" class="row-items"/>
                    <TextField v-model="decimeters" class="row-items row-input-text input"/>
                    <Button text="<=>" @tap="reverse()" class="button"/>
                    <Label text="to foots:" class="row-items"/>
                    <Label v-model="foots" class="row-items row-input-text"/>
                </StackLayout>
                <Button text="Convert" @tap="convert()" class="button" />
            </template>
            <Keyboard class="keyboard"
                :firstValue="foots"
                :secondValue="decimeters"
                :reverseStatus="reverseStatus"
                @updateParents="update"
            />
        </StackLayout>
    </Page>
</template>

<script>
import lengthPage from '../Length/LengthPage.vue'
import Keyboard from '../Keyboard.vue'
    export default {
    data() {
        return {
            foots: '',
            decimeters: '',
            footDec: '3',
            reverseStatus: true,
            lengthPage: lengthPage,
        }
    },
    components: {Keyboard},
    methods: {
        reverse() {
            this.reverseStatus = !this.reverseStatus
            this.foots = this.decimeters = ''     
        },
        convert() {
            if (this.reverseStatus === false) {
                if (this.decimeters === '') {
                    return
                }
                else {
                    this.foots = this.decimeters/this.footDec
                    if (isNaN(this.foots)) {
                        this.foots = 'Error'
                    }
                }
            }
            if (this.reverseStatus === true) {
                if (this.foots === '') {
                    return
                }
                else {
                    this.decimeters = this.foots*this.footDec
                    if (isNaN(this.decimeters)) {
                        this.decimeters = 'Error'
                    }
                }
            } 
        },
        update(data) {
            this.foots = data.first
            this.decimeters = data.second
        }
    },
};
</script>

<style src="@/style.css"></style>