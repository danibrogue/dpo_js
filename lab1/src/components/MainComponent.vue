<script>
    export default {
        name: "MainComponent",
        data() {
            return {
                v_feet: "",
                v_metres: "",
                v_nmi: "",
                v_kilometres: "",
                v_deg: "",
                v_rad: "",
                v_celsium: "",
                v_fahrenheit: ""
            };
        },
        computed: {
            metres_value : {
                get: function(){
                    return this.v_feet * 0.3048;
                }
            },
            feet_value : {
                get: function(){
                    return this.v_metres / 0.3048;
                }
            },
            kilometres_value : {
                get: function(){
                    return this.v_nmi * 1.852;
                }
            },
            naval_miles_value : {
                get: function(){
                    return this.v_kilometres / 1.852;
                }
            },
            radians_value : {
                get: function(){
                    return this.v_deg * Math.PI / 180;
                }
            },
            degrees_value : {
                get: function(){
                    return this.v_rad * 180 / Math.PI;
                }
            },
            fahrenheit_value : {
                get: function(){
                    return this.v_celsium * 9 / 5 + 32;
                }
            },
            celsium_value : {
                get: function(){
                    return (this.v_fahrenheit - 32) * 5 / 9;
                }
            }
                    
        }
    }
</script>

<template>
    <div class="main">
        <p>feet-metres</p>
        <div class="metrics">
            <input type="number" id="feet" v-model.number="v_feet" v-bind:placeholder="feet_value" />
            <input type="number" id="metres" v-model.number="v_metres" v-bind:placeholder="metres_value" />
        </div>

        <p>naval miles-kilometres</p>
        <div class="metrics">
            <input type="number" id="nmi" v-model.number="v_nmi" v-bind:placeholder="naval_miles_value" />
            <input type="number" id="km" v-model.number="v_kilometres" v-bind:placeholder="kilometres_value" />
        </div>

        <p>degrees-radians</p>
        <div class="metrics">
            <input type="number" id="deg" v-model.number="v_deg" v-bind:placeholder="degrees_value" />
            <input type="number" id="rad" v-model.number="v_rad" v-bind:placeholder="radians_value" />
        </div>

        <p>celsium-fahrenheit</p>
        <div class="metrics">
            <input type="number" id="celsium" v-model.number="v_celsium" v-bind:placeholder="celsium_value" />
            <input type="number" id="fahrenheit" v-model.number="v_fahrenheit" v-bind:placeholder="fahrenheit_value" />
        </div>
    </div> 
</template>

<style>
    .metrics {
        display: flex;
        flex-direction: row;
        justify-content: center;
    }

    input[type=number] {
    width: 150px;
    height: 35px;
    margin: 7px;
    border: 1.75px solid black;
    border-radius: 5px;
    box-sizing: border-box;
    font-family: 'Red Ring';
}
</style>
