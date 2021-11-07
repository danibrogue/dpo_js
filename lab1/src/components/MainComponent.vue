<template>
    <div class="main">
        <div class="metrics">
            <input type="number" v-model.number="feet" placeholder="ft" />
            <p>{{ metres_value + " m" }}</p>
        </div>
        <div class="metrics">
            <input type="number" v-model.number="nmi" placeholder="nmi" />
            <p>{{ kilometres_value + " km" }}</p>
        </div>
        <div class="metrics">
            <input type="number" v-model.number="deg" placeholder="degrees" />
            <p>{{ radians_value + " rad" }}</p>            
        </div>
        <div class="metrics">
            <input type="number" v-model.number="celsium" placeholder="°C" />
            <p>{{ fahrenheit_value + " °F" }}</p>                 
        </div>
    </div> 
</template>

<script>
    export default {
        name: "MainComponent",
        data() {
            return {
                feet: "",
                nmi: "",
                deg: "",
                celsium: ""
            };
        },
        computed: {
            metres_value : {
                get: function(){
                    return this.feet * 0.3048;
                }
            },
            kilometres_value : {
                get: function(){
                    return this.nmi * 1.852;
                }
            },
            radians_value : {
                get: function(){
                    return this.deg * Math.PI / 180;
                }
            },
            fahrenheit_value : {
                get: function(){
                    return this.celsium === "" ? 0 : this.celsium * 9 / 5 + 32;
                }
            }            
        }
    }
</script>

<style>
    input[type=number] {
    width: 300px;
    height: 35px;
    margin: 7px;
    border: 1.75px solid black;
    border-radius: 5px;
    box-sizing: border-box;
    font-family: 'Red Ring';
}
</style>
