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
                    <Label text="to tons:" class="row-items"/>
                    <Label v-model="tons" editable="false" class="row-items row-input-text"/>
                </StackLayout>
                <Button text="Convert" @tap="convert()" class="button" />
            </template>
            <template v-else>
                <StackLayout>
                    <Label text="from tons:" class="row-items"/>
                    <TextField v-model="tons" editable="false" class="row-items row-input-text input"/>
                    <Button text="<=>" @tap="reverse()" class="button"/>
                    <Label text="to kilograms:" class="row-items"/>
                    <Label v-model="kilograms" editable="false" class="row-items row-input-text"/>
                </StackLayout>
                <Button text="Convert" @tap="convert()" class="button" />
            </template>
            <Keyboard class="keyboard"
                :firstValue="kilograms"
                :secondValue="tons"
                :reverseStatus="reverseStatus"
                @updateParents="update"
            />
        </StackLayout>
    </Page>
</template>

<script>
import Keyboard from '../Keyboard.vue'
import WeightPage from '../Weight/WeightPage.vue'
    export default {
    data() {
        return {
            kilograms: '',
            tons: '',
            reverseStatus: true,
            WeightPage: WeightPage,
        }
    },
    components: {Keyboard},
    methods: {
        reverse() {
            this.reverseStatus = !this.reverseStatus
            this.kilograms = this.tons = ''     
        },
        convert() {
            if (this.reverseStatus === false)
            {
                this.kilograms = this.tons*1000
                if (isNaN(this.kilograms)) {
                    this.kilograms = 'Error'
                }
            }
            if (this.reverseStatus === true) {
                this.tons = this.kilograms/1000
                if (isNaN(this.tons)) {
                    this.tons = 'Error'
                }
            } 
        },
        update(data) {
            this.kilograms = data.first
            this.tons = data.second
        }
    },
};
</script>

<style src="@/style-converter.css"></style>