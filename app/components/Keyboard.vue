<template>
    <WrapLayout class="keyboard">
        <Button v-for="number in numbers" @tap="input(number)" class="button-keyboard">{{number}}</Button>
        <Button text="<=" @tap="clearChar()" class="button-keyboard"></Button>
        <Button text="C" @tap="clearInput()" class="button-keyboard" style="width: 93%;"></Button>
    </WrapLayout>
</template>

<script>

    export default {
        data() {
            return {
                numbers: ['1', '2', '3', '4', '5', '6', '7', '8', '9', '0', '.'],
                first: '',
                second: '',
            }
        },
        props: ['firstValue', 'secondValue', 'reverseStatus'],
        methods: {
            input(char) {
                if (this.reverseStatus === true) {
                    this.firstValue += char        
                }
                if (this.reverseStatus === false) {
                    this.secondValue += char    
                }
                this.update()    
            },
            clearInput() {
                if (this.reverseStatus === true) {
                    this.firstValue = ''    
                }
                if (this.reverseStatus === false) {
                    this.secondValue = '' 
                }
                this.update()    
            },
            clearChar() {
                if (this.reverseStatus === true) {
                    this.count = String(this.firstValue).length
                    this.convertText = String(this.firstValue)
                    this.firstValue = (this.convertText).substr(0, this.count - 1)
                }
                if (this.reverseStatus === false) {
                    this.count = String(this.secondValue).length
                    this.convertText = String(this.secondValue)
                    this.secondValue = (this.convertText).substr(0, this.count - 1)
                }
                this.update() 
            },
            update() {
                this.$emit('updateParents', {
                    first: this.firstValue,
                    second: this.secondValue
                })
            }
        },
    }
</script>

<style src="@/style-converter.css"></style>