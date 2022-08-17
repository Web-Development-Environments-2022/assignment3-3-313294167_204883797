<template>
  <form ref="form" @submit.stop.prevent="handleSubmit">
        <b-form-group
          label="Title"
          label-for="title-input"
          invalid-feedback="Title is required"
        >
          <b-form-input
            id="title"
            v-model="title"
            required
          ></b-form-input>
        </b-form-group>

        <b-form-group
          label="Minutes"
          label-for="minutes-input"
          invalid-feedback="Minutes is required"
        >
          <b-form-input
            id="minutes"
            v-model="minutes"
            required
          ></b-form-input>
        </b-form-group>


<!-- need to be array option -->        
        <b-form-group
          label="Steps"
          label-for="steps-input"
          invalid-feedback="Steps is required"
        >
          <b-form-input
            id="steps"
            v-model="steps"
            required
          ></b-form-input>
        </b-form-group>


<!-- need to be array option -->        
        <b-form-group
          label="Ingredients"
          label-for="ingredients-input"
          invalid-feedback="Ingredients is required"
        >
          <b-form-input
            id="ingredients"
            v-model="ingredients"
            required
          ></b-form-input>
        </b-form-group>


<!-- need to be link to image or upload img-->        
        <b-form-group
          label="Image"
          label-for="image-input"
          invalid-feedback="Image is required"
        >
          <b-form-input
            id="image"
            v-model="image"
            required
          ></b-form-input>
        </b-form-group>

        <b-form-group
          id="input-group-vegan"
          label-cols-sm="3"
          label="vegan"
          label-for="vegan"
        >
          <b-form-select
            id="vegan"
            v-model="vegan"
            :options="vegan"
          ></b-form-select>
        </b-form-group>

        <b-form-group
          id="input-group-vegetarian"
          label-cols-sm="3"
          label="vegetarian-label"
          label-for="vegetarian"
        >
          <b-form-select
            id="vegetarian"
            v-model="vegetarian"
            :options="vegetarian"
          ></b-form-select>
        </b-form-group>

        <b-form-group
          id="input-group-gluten"
          label-cols-sm="3"
          label="gluten-label"
          label-for="gluten"
        >
          <b-form-select
            id="gluten"
            v-model="gluten"
            :options="gluten"
          ></b-form-select>
        </b-form-group>

      </form>
</template>

<script>
export default {
    name: "Modal",
    data() {
      return {
      form: {
        title : "",
        minutes: "",
        image: "",
        vegan: "",
        vegetarian: "",
        glutenFree: "",
        steps:"",
        ingredients: "",
      },
      vegan: [
          { value: "yes", text: 'yes' },
          { value: "no", text: 'no' },
        ],
        vegetarian: [
          { value: "yes", text: 'yes' },
          { value: "no", text: 'no' },
        ],
        gluten: [
          { value: "yes", text: 'yes' },
          { value: "no", text: 'no' },
        ],
      
    };
    },
    methods: {
      async handleSubmit() {
        try {
        
        const response = await this.axios.post(
          this.$root.store.server_domain +"/users/personal",
          {
            title: this.form.title,
            readyInMinutes: this.form.minutes,
            image: this.form.image,
            vegan: this.form.vegan,
            vegetarian: this.form.vegetarian,
            glutenFree: this.form.glutenFree,
            steps: this.form.steps,
            ingredients: this.form.ingredients
          }
        );
        console.log(response)
        // console.log(response);
        // this.$root.loggedIn = true;
      } catch (err) {
        console.log(err.response);
        this.form.submitError = err.response.data.message;
      }
        

      },
    //   validateState(param) {
    //   const { $dirty, $error } = this.$v.form[param];
    //   return $dirty ? !$error : null;
    // },
    }
    }
</script>

<style>

</style>