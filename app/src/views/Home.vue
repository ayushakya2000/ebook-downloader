<template>
  <v-parallax src="https://firebasestorage.googleapis.com/v0/b/new111-87012.appspot.com/o/book-stack-books-education-48126.jpg?alt=media&token=4764ddac-164d-47ec-9f3e-8556f90ed311" height="100%">
  <v-app style="background: rgb(0,0,0,0)">
    <v-toolbar app color="rgb(0,0,0,0.5)">
      <v-toolbar-title class="headline text-uppercase" dark>
        <span>get</span>
        <span class="font-weight-light white--text">placed</span>
      </v-toolbar-title>
    </v-toolbar>
    <br>
    <v-img aspect-ratio contain max-width="55%" src="https://firebasestorage.googleapis.com/v0/b/new111-87012.appspot.com/o/untitled%20(2).svg?alt=media&token=6befa2a0-9d68-4cad-a3ec-23416867239c"></v-img>
    <v-layout align-center justify-start>
      <v-flex xs10 sm6 md5 lg4 offset-xs1 offset-md1 offset-lg1>
        <form>
          <v-text-field
            
            v-model="name"
            :error-messages="nameErrors"
            :counter="25"
            label="Name"
            required
            @input="$v.name.$touch()"
            @blur="$v.name.$touch()"
          ></v-text-field>
          <v-text-field
            
            v-model="jobProfile"
            :error-messages="jobProfileErrors"
            :counter="50"
            label="Job Profile"
            required
            @input="$v.jobProfile.$touch()"
            @blur="$v.jobProfile.$touch()"
          ></v-text-field>
          <v-text-field
            
            v-model="jobLocation"
            :error-messages="jobLocationErrors"
            :counter="20"
            label="Expected Job Location"
            required
            @input="$v.jobLocation.$touch()"
            @blur="$v.jobLocation.$touch()"
          ></v-text-field>

          <v-text-field
            
            v-model="salary"
            :error-messages="salaryErrors"
            :counter="10"
            label="Expected Salary"
            required
            @input="$v.salary.$touch()"
            @blur="$v.salary.$touch()"
          ></v-text-field>

          <v-text-field
            
            v-model="city"
            :error-messages="cityErrors"
            :counter="10"
            label="Current City"
            required
            @input="$v.city.$touch()"
            @blur="$v.city.$touch()"
          ></v-text-field>

          <v-text-field
            
            v-model="phone"
            :error-messages="phoneErrors"
            :counter="10"
            label="Phone Number"
            required
            @input="$v.phone.$touch()"
            @blur="$v.phone.$touch()"
          ></v-text-field>

          <v-text-field
            
            v-model="email"
            :error-messages="emailErrors"
            label="E-mail"
            required
            @input="$v.email.$touch()"
            @blur="$v.email.$touch()"
          ></v-text-field>
          <!--     <v-select
          v-model="select"
          :items="items"
          :error-messages="selectErrors"
          label="Item"
          required
          @change="$v.select.$touch()"
          @blur="$v.select.$touch()"
          ></v-select> 
          -->
          <v-checkbox
          
            v-model="checkbox"
            :error-messages="checkboxErrors"
            label="Do you agree?"
            required
            @change="$v.checkbox.$touch()"
            @blur="$v.checkbox.$touch()"
          ></v-checkbox>
          <v-layout justify-center>
              <v-btn outline large color="indigo" @click="submit">submit</v-btn>
              <v-btn outline large color="indigo" @click="clear">clear</v-btn>
          </v-layout>
        </form>
      </v-flex>
    </v-layout>
  </v-app>
  </v-parallax>
</template>

<script>
import { validationMixin } from "vuelidate";
import {
  required,
  maxLength,
  email,
  numeric,
  alpha
} from "vuelidate/lib/validators";
import firebase from "firebase";


export default {
  mixins: [validationMixin],

  validations: {
    name: { required, maxLength: maxLength(25), alpha },
    city: { required, maxLength: maxLength(10), alpha },
    jobProfile: { required, maxLength: maxLength(50), alpha },
    jobLocation: { required, maxLength: maxLength(20), alpha },
    salary: { required, maxLength: maxLength(10), numeric },
    phone: { required, maxLength: maxLength(10), numeric },
    email: { required, email },
    // select: { required },
    checkbox: {
      checked(val) {
        return val;
      }
    }
  },

  data: () => ({
    name: "",
    email: "",
    jobLocation: "",
    jobProfile: "",
    salary: "",
    phone: "",
    city: "",
    /*      select: null,
      items: [
        'Item 1',
        'Item 2',
        'Item 3',
        'Item 4'
        ],*/
    checkbox: false
  }),

  computed: {
    checkboxErrors() {
      const errors = [];
      if (!this.$v.checkbox.$dirty) return errors;
      !this.$v.checkbox.checked && errors.push("You must agree to continue!");
      return errors;
    },
    /*      selectErrors () {
        const errors = []
        if (!this.$v.select.$dirty) return errors
        !this.$v.select.required && errors.push('Item is required')
        return errors
    },*/
    nameErrors() {
      const errors = [];
      if (!this.$v.name.$dirty) return errors;
      !this.$v.name.maxLength &&
        errors.push("Name must be at most 25 characters long");
      !this.$v.name.alpha && errors.push("Must be alphabets only.");
      !this.$v.name.required && errors.push("Name is required.");
      return errors;
    },
    cityErrors() {
      const errors = [];
      if (!this.$v.city.$dirty) return errors;
      !this.$v.city.maxLength &&
        errors.push("Current City must be at most 25 characters long");
      !this.$v.city.required && errors.push("City is required.");
      !this.$v.city.alpha && errors.push("Must be alphabets only.");
      return errors;
    },
    jobProfileErrors() {
      const errors = [];
      if (!this.$v.jobProfile.$dirty) return errors;
      !this.$v.jobProfile.maxLength &&
        errors.push("Job Profile must be at most 50 characters long");
      !this.$v.jobProfile.required && errors.push("Job Profile is required.");
      !this.$v.jobProfile.alpha && errors.push("Must be alphabets only.");
      return errors;
    },
    jobLocationErrors() {
      const errors = [];
      if (!this.$v.jobLocation.$dirty) return errors;
      !this.$v.jobLocation.maxLength &&
        errors.push("Expected Job Location must be at most 10 characters long");
      !this.$v.jobLocation.required &&
        errors.push("Expected Job Location is required.");
      !this.$v.jobLocation.alpha && errors.push("Must be alphabets only.");
      return errors;
    },
    emailErrors() {
      const errors = [];
      if (!this.$v.email.$dirty) return errors;
      !this.$v.email.email && errors.push("Must be valid e-mail");
      !this.$v.email.required && errors.push("E-mail is required");
      return errors;
    },

    salaryErrors() {
      const errors = [];
      if (!this.$v.salary.$dirty) return errors;
      !this.$v.salary.numeric && errors.push("Must be number");
      !this.$v.salary.required && errors.push("Salary is required");
      !this.$v.salary.maxLength &&
        errors.push("Must be of length less than 10.");
      return errors;
    },
    phoneErrors() {
      const errors = [];
      if (!this.$v.phone.$dirty) return errors;
      !this.$v.phone.numeric && errors.push("Must be number");
      !this.$v.phone.required && errors.push("Phone Number is required");
      !this.$v.phone.maxLength &&
        errors.push("Must be of length less than 10.");
      return errors;
    }
  },

  methods: {
    submit() {
      this.$v.$touch();
    },
    clear() {
      this.$v.$reset();
      this.name = "";
      this.email = "";
      this.jobProfile = "";
      this.jobLocation = "";
      this.salary = "";
      this.phone = "";
      this.city = "";
      // this.select = null
      this.checkbox = false;
    }
  }
};
</script>
Chat conversation end
Type a message...

