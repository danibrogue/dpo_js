<template>
    <transition>
        <form v-if="info.VisibleResume">
            <div class="topBlock">
                <div class="info">
                    <p>{{info.FirstName}} {{info.LastName}}</p>
                    <p>{{age}}, родился {{info.Birthday}}</p>
                    <p style="font-size: 24px;">Контакты</p>
                    <p>+7{{info.PhoneNumber}}</p>
                    <p>{{info.Email}}</p>
                    <p>Место проживания: {{info.Location}}</p>
                </div>
                <div class="photo">
                    <img
                        :src= "info.Image"
                        alt="..."
                        width="200"
                        height="200">
                </div>
            </div>
            <div class="bottomBlock">
                <div class="about">
                    <p style="font-size: 24px">Образование</p>
                    <div v-for="(Edu, index) in info.Education">
                        <p>{{info.Education[index].classEdu}}</p>
                        <div v-if="info.Education[index].classEdu != 'Среднее'">
                            <p style="font-size: 24px">Учебное заведение</p>
                            <p>{{info.Education[index].CollegeName}}</p>
                            <p style="font-size: 24px">Факультет</p>
                            <p>{{info.Education[index].Faculty}}</p>
                            <p style="font-size: 24px">Специальность</p>
                            <p>{{info.Education[index].Specialization}}</p>
                            <p style="font-size: 24px">Год окончания</p>
                            <p>{{info.Education[index].GradYear}}</p>
                        </div>
                    </div>
                    <p style="font-size: 24px">Ключевые навыки</p>
                    <p>{{info.KeySkills}}</p>
                    <p style="font-size: 24px">О себе</p>
                    <p>{{info.AboutMe}}</p>
                </div>
                <div class="salary">
                    <p style="font-size: 24px">Желаемая зарплата</p>
                    <p>{{info.Salary}}</p>
                    <p style="font-size: 24px">Статус</p>
                    <select>
                        <option selected>Новый</option>
                        <option>Назначено собеседование</option>
                        <option>Принят</option>
                        <option>Отказ</option>
                    </select>
                </div>
            </div>
        </form>
    </transition>
</template>

<script>
    export default{
        name: "OutputForm",
        props: {
            info: Object
        },
        computed: {
            age : {
                get:function () {
                    let now= new Date();
                    let old=new Date(this.info.Birthday.replace('/(\d{4})\.(\d{2})\.(\d{2})/)','$1-$2-$3'));
                    let year=new Date(now - old)
                    return year.getUTCFullYear()-1970;
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
        margin-top: 30px;
    }
    .photo {
        width: 200px;
        height: 200px;
        margin-top: 10px;
    }

    .topBlock {
        width: 600px;
        margin: auto;
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        margin-top: 10px;
        text-align: left;
    }

    .bottomBlock {
        width: 600px;
        margin: auto;
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        margin-top: 10px;
        text-align: left;
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
</style>
