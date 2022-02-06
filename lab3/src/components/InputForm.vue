<template>
    <form>
        <div class="photoBlock">
            <div>
                <p>Ссылка на фото</p>
                <textarea v-model="info.Image"></textarea>
            </div>
            <div>
                <img
                    :src="info.Image"
                    alt="..."
                    width="250" 
                    height="250">
            </div>
        </div>

        <div class="contacts">
            <p>Контактные данные</p>
            <div class="inputField">
                <p>Имя</p>
                <input v-model="info.FirstName">
            </div>
            <div class="inputField">
                <p>Фамилия</p>
                <input v-model="info.LastName">
            </div>
            <div class="inputField">
                <p>Номер телефона</p>
                <input v-model="info.PhoneNumber" @blur="info.PhoneEdited = true;" v-bind:placeholder="8005553535">
            </div>
            <transition>
                <div v-if="PhoneError">
                    <p>Некорректный номер телефона</p>
                </div>
            </transition>
            <div class="inputField">
                <p>E-mail</p>
                <input v-model="info.Email">
            </div>
            <div class="inputField">
                <p>Город проживания</p>
                <input v-model="info.Location">
            </div>
        </div>

        <div class="information">
            <div class="inputField">
                <p>Дата рождения</p>
                <input v-model="info.Birthday">
            </div>
            <div class="inputField">
                <p>Желаемая зарплата</p>
                <input v-model="info.Salary">
            </div>
            <div class="inputField">
                <p>Образование</p>
                <select v-on:change="OnChange" v-model="info.Education">
                    <option value="Среднее">Среднее</option>
                    <option value="Среднее специальное">Среднее специальное</option>
                    <option value="Неоконченное высшее">Неоконченное высшее</option>
                    <option value="Высшее">Высшее</option>
                </select>
            </div>
            <transition>
                <div v-if="info.Education != 'Среднее'">
                    <div class = "inputField">
                        <p>Учебное заведение</p>
                        <input v-model="info.CollegeName">
                    </div>
                    <div class = "inputField">
                        <p>Факультет</p>
                        <input v-model="info.Faculty">
                    </div>
                    <div class = "inputField">
                        <p>Специальность</p>
                        <input v-model="info.Specialization">
                    </div>
                    <div class = "inputField">
                        <p>Год окончания</p>
                        <input v-model="info.GradYear">
                    </div>
                </div>
            </transition>
            <div class="inputField" style="margin-bottom: 10px;">
                <p>Ключевые навыки</p>
                <textarea v-model="info.KeySkills" style="width: 292.5px"></textarea>
            </div>
            <div class="inputField">
                <p>О себе</p>
                <textarea v-model="info.AboutMe" style="height: 75px; width: 292.5px"></textarea>
            </div>
        </div>

        <button type="button" v-on:click="info.VisibleResume = !info.VisibleResume">
            {{ButtonMessage}}
        </button>
    </form>
</template>

<script>
    export default{
        name: "InputForm",
        props: {
            info: Object
        },
        computed: {
            ButtonMessage: function() {
                return this.info.VisibleResume ? 'Скрыть резюме' : 'Показать резюме';
            },
            PhoneError() {
                if(this.info.PhoneEdited){
                    return this.info.PhoneNumber.length < 6 ||
                    this.info.PhoneNumber.length > 10 ||
                    isNaN(this.info.PhoneNumber);
                }
            }
        },
        methods: {
            OnChange(){
                if(this.info.Education == 'Среднее'){
                    this.info.Faculty = ''
                    this.info.CollegeName = ''
                    this.info.Specialization = ''
                    this.info.GradYear = ''
                }
            }
        }
    }
</script>


<style>
    form {
        border: 1.75px solid black;
        border-radius: 5px;
        width: 900px;
        margin: auto;
    }
    .photoBlock {
        width: 600px;
        margin: auto;
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        margin-top: 10px;
    }

    .inputField {
        width: 700px;
        margin: auto;
        display: flex;
        flex-direction: row;
        justify-content: space-between;
    }


    textarea {
        border: 1.75px solid black;
        border-radius: 5px;
        font-family: 'Red Ring';
        width: 150px;
        height: 50px;
    }

    img {
        border-radius: 5px;
    }

    input {
        width: 300px;
        height: 35px;
        margin-bottom: 7px;
        margin-top: 7px;
        border: 1.75px solid black;
        border-radius: 5px;
        box-sizing: border-box;
        font-family: 'Red Ring';
    }

    select {
        width: 300px;
        height: 35px;
        margin-bottom: 7px;
        margin-top: 7px;
        border: 1.75px solid black;
        border-radius: 5px;
        box-sizing: border-box;
        font-family: 'Red Ring';
    }

    button[type=button] {
        background-color: black;
        width: 150px;
        height: 25px;
        margin: 7px;
        border: 1.75px solid black;
        border-radius: 5px;
        box-sizing: border-box;
        font-family: 'Red Ring';
        color: white;
    }
</style>