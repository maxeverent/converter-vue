<template>
    <Page class="body">
        <ActionBar>
            <Label text="Converter" class="header" />
        </ActionBar>
        <StackLayout>
            <Button text="Back" @tap="$navigateTo(lengthPage)" class="button" style="margin-top: 30px;" />          
            <template v-if="reverseStatus" >
                <StackLayout>
                    <Label text="from kilometers:" class="row-items"/>
                    <TextField v-model="kilometers" class="row-items row-input-text input"/>
                    <Button text="<=>" @tap="reverse()" class="button"/>
                    <Label text="to foot:" class="row-items"/>
                    <Label v-model="foots" class="row-items row-input-text"/>
                </StackLayout>
                <Button text="Convert" @tap="convert()" class="button" />
            </template>
            <template v-else>
                <StackLayout>
                    <Label text="from foot:" class="row-items"/>
                    <TextField v-model="foots" class="row-items row-input-text input"/>
                    <Button text="<=>" @tap="reverse()" class="button"/>
                    <Label text="to kilometers:" class="row-items"/>
                    <Label v-model="kilometers" class="row-items row-input-text"/>
                </StackLayout>
                <Button text="Convert" @tap="convert()" class="button" />
            </template>
            <Keyboard class="keyboard"
                :firstValue="kilometers"
                :secondValue="foots"
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
            kilometers: '',
            foots: '',
            foot: '3280.8',
            reverseStatus: true,
            lengthPage: lengthPage,
        }
    },
    components: {Keyboard},
    methods: {
        reverse() {
            this.reverseStatus = !this.reverseStatus
            this.kilometers = this.foots = ''     
        },
        convert() {
            if (this.reverseStatus === false) {
                if (this.foots === '') {
                    return
                }
                else {
                    this.kilometers = this.foots/this.foot
                    if (isNaN(this.kilometers)) {
                        this.kilometers = 'Error'
                    }
                }
            }
            if (this.reverseStatus === true) {
                if (this.kilometers === '') {
                    return
                }
                else {
                    this.foots = this.kilometers*this.foot
                    if (isNaN(this.foots)) {
                        this.foots = 'Error'
                    }
                }
            } 
        },
        update(data) {
            this.kilometers = data.first
            this.foots = data.second
        }
    },
};
</script>

<style src="@/style-converter.css"></style>