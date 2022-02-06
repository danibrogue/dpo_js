<template>
  <div>
    <InputForm :info="info"></InputForm>
    <OutputForm :info="info"></OutputForm>
  </div>
</template>

<script>
  import InputForm from "./InputForm.vue";
  import OutputForm from "./OutputForm.vue";
  import axios from 'axios';
  export default {
    name: 'MainComponent',
    components: {OutputForm, InputForm},
    data () {
      return {
        info: {
          errors: [],
          Image: undefined,
          Education: [{classEdu: 'Среднее', CollegeName:'', Faculty: '', Specialization: '', GradYear: ''}],
          PhoneNumber: '',
          PhoneEdited: false,
          FirstName: '',
          LastName: '',
          Birthday: '',
          Email: '',
          Location: '',
          Salary: '',
          KeySkills: '',
          AboutMe: '',
          VisibleResume: false,
          VkCity: '{ "id":, "title":, "important": 1 }',
          VkUniversities: '{"id":,"title":,"important":1}'
          // токен - 81476b021a2da4d6b11a92b177d72c64ca1a1414b4b7aa439d170ebe47607e9a0a0249a0cec8cfb34870d
        }
      }
    }
  }
</script>