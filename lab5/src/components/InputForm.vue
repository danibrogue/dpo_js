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
                <input 
                    v-model="info.Location" 
                    v-on:change="OnChangeLocation" 
                    v-on:input="OnChangeLocation"
                    list="dataLocation"
                >
                <datalist id="dataLocation">
                    <option v-for="item of info.VkCity" :value="item.title" :key="item.id"></option>
                </datalist>
            </div>
        </div>

        <div class="information">
            <div class="inputField">
                <p>Дата рождения</p>
                <input type="date" v-model="info.Birthday">
            </div>
            <div class="inputField">
                <p>Желаемая зарплата</p>
                <input v-model="info.Salary">
            </div>
            <div v-for="(Edu, index) in info.Education">
                <div class="inputField">
                    <p>Образование</p>
                    <div class="additionalEdu">
                        <div v-if="index!=0">
                            <button 
                                id="crossButton"
                                type="button" 
                                v-on:click="info.Education.splice(index,1)"
                                >
                                Х
                            </button>
                        </div>
                        <select v-on:change="OnChange" v-model="info.Education[index].classEdu">
                            <option value="Среднее">Среднее</option>
                            <option value="Среднее специальное">Среднее специальное</option>
                            <option value="Неоконченное высшее">Неоконченное высшее</option>
                            <option value="Высшее">Высшее</option>
                        </select>
                    </div>
                </div>
                <transition>
                    <div v-if="info.Education[index].classEdu != 'Среднее'">
                        <div class = "inputField">
                            <p>Учебное заведение</p>
                            <input 
                                v-model="info.Education[index].CollegeName"
                                v-on:input="OnInputUniversities"
                                list="dataUniversities"
                            >
                            <datalist id="dataUniversities">
                                <option v-for="item of info.VkUniversities" :value="item.title" :key="item.id"></option>
                            </datalist>
                        </div>
                        <div class = "inputField">
                            <p>Факультет</p>
                            <input v-model="info.Education[index].Faculty">
                        </div>
                        <div class = "inputField">
                            <p>Специальность</p>
                            <input v-model="info.Education[index].Specialization">
                        </div>
                        <div class = "inputField">
                            <p>Год окончания</p>
                            <input v-model="info.Education[index].GradYear">
                        </div>
                    </div>
                </transition>
            </div>
            <div>
                <button
                    type="button"
                    v-on:click="info.Education.push({classEdu: 'Среднее', CollegeName: '', Faculty: '', Specialization: '', GradYear: ''})"
                    style="width: 200px;"
                >
                Добавить образование
                </button>
            </div>
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
    import axios from 'axios';
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
            onChange(){
                for(let i=0;i<this.info.Education.length;++i){
                    if(this.info.Education[i].classEdu == 'Среднее') {
                        this.info.Education[i].Faculty = ''
                        this.info.Education[i].EduInstitution = ''
                        this.info.Education[i].Specialization = ''
                        this.info.Education[i].YearEnd = ''
                    }
                }
            },
            OnChangeLocation(){
                 axios.get("https://api.vk.com/method/database.getCities?" +
                  "country_id=1&" +
                  "q=" +this.info.Location +
                  "&need_all=1&" +
                  "count=10&" +
                  "access_token=8c4207a095f73d7ecea73c7041c94000275926e3cbd2919290b5adf3bce41dcba52caf1599f0fa22d0126&" +
                  "v=5.131")
                  .then(response => this.info.VkCity=response.data.response.items);
                  console.log(this.info.VkCity);
            },
            OnInputUniversities() {
                axios.get('https://api.vk.com/method/database.getUniversities?' +
                    'country_id=1&' +
                    'city_id='+ this.idLocation[0].id+
                    '&count=10&' +
                    'access_token=16bd660e592e5759f2a2cdccd3562b4c8613fb4d03cb49ed0012b38f57f4878a9108d6d50d6bc7c6624c9&' +
                    'v=5.131')
                    .then(response=>this.info.VkUniversities=response.data.response.items)
            }
        },
        mounted() {
            
        }
    }
</script>


<style>
    #crossButton {
        width: 35px;
        height: 35px;
        margin: 0px;
        margin-top: 7px;
    }
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

    .additionalEdu {
        display: flex;
        flex-direction: row;
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