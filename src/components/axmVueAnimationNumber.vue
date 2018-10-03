<template>
    <div :class="customclass">{{ displayNumber(valueAnimate) }}</div>
</template>

<script>
    export default {
        name: 'axmVueAnimationNumber',
        props: ['number', 'customclass', 'duration'],
        data: function () {
            return {
                value: null,
                valueAnimate: 0,
            }
        },
        mounted: function () {
            this.value = this.number;
            if(this.value != null && this.value != '' && this.value != undefined){

                this.value = parseFloat(this.value);

                if(this.value != NaN){

                    let that = this;
                    let myTimer;
                    let delay = 9;
                    let adition = 1;

                    if(this.value < 0){
                        this.isNegative = true;
                    }

                    if(this.duration > 0){
                        let tmpDelay = this.duration / delay;
                        adition = Math.abs(this.value) / tmpDelay;
                    }else{
                        delay = 0;
                    }

                    myTimer = setInterval(function(){
                        if((that.valueAnimate+=adition) < Math.abs(that.value)){
                            that.valueAnimate += adition;
                        }else{
                            clearInterval(myTimer)
                            that.valueAnimate = Math.abs(that.value);
                        }
                    }, delay);
                }
            }
        },
        methods: {
            countDecimals: function (value) {
                if (Math.floor(value) === value) {
                    return 0;
                }
                return value.toString().split(".")[1].length || 0;
            },
            displayNumber: function (value) {
                if (value != null && value != '' && value != undefined && value != NaN) {
                    return (this.isNegative ? '-' : '') + value.toFixed(this.countDecimals(this.value));
                }
            }
        }
    }
</script>

<style scoped>
</style>
