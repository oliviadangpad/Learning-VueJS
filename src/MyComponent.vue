<template>
    <form @submit.prevent="handleSubmit">
      <h2>{{ greetingMessage }}</h2>
      <label>
        First Name:
        <input type="text" v-model="formData.firstName" placeholder="First Name" />
        <div v-if="!isValidFirstName" class="error">Please enter a valid first name</div>
  
      </label>
      <label>
        Last Name:
        <input type="text" v-model="formData.lastName" placeholder="Last Name" />
        <div v-if="!isValidLastName" class="error">Please enter a valid last name</div>
  
      </label>
  
      <br />
      <div v-if="errorMessage">{{ errorMessage }}</div>
      <button type="submit" :disabled="!isFormValid">Submit</button>
    </form>
  </template>
  
  <script setup lang="ts">
  import { reactive, computed, ref } from 'vue';
  
  interface Props {
    greetingMessage: string
    bar?: number
  }
  
  const {greetingMessage} = defineProps<Props>()
  
  interface FormData {
    firstName: string;
    lastName: string;
  }
  
  // Define reactive state for form data
  const formData = reactive<FormData>({ firstName: '', lastName: '' })
  
  // Define computed properties for form validation
  const isValidFirstName = computed(() => formData.firstName);
  const isValidLastName = computed(() => formData.lastName);
  const isFormValid = computed(() => isValidFirstName.value && isValidLastName.value);
  
  
  // error message
  const errorMessage = ref('');
  
  const handleSubmit = () => {
    try {
      onSubmit(formData);
    } catch (error) {
      errorMessage.value = 'An error occurred while submitting the form';
      console.error(error);
    }
  
  };
  
  const onSubmit = ({ firstName, lastName }) => {
    // Perform form submission logic here
    alert(JSON.stringify(firstName, lastName))
  }
  </script>
  