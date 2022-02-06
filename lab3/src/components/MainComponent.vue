<template>
  <div>
    <InputForm :info="info"></InputForm>
    <OutputForm :info="info"></OutputForm>
  </div>
</template>

<script>
  import InputForm from "./InputForm.vue";
  import OutputForm from "./OutputForm.vue";
  export default {
    name: 'MainComponent',
    components: {OutputForm, InputForm},
    data () {
      return {
        info: {
          errors: [],
          Image: undefined,
          Education: '',
          Faculty: '',
          CollegeName: '',
          Specialization: '',
          GradYear: '',
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
          VisibleResume: false
        }
      }
    }
  }
</script>