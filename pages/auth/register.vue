<script setup>
import { useForm, useField } from "vee-validate";
import * as yup from "yup";
import { useRouter } from "#app";

// Initialize Nuxt Router (Handled in layouts, but included for redirects)
const router = useRouter();

// Define validation schema using Yup
const validationSchema = yup.object({
  fullname: yup.string().min(2, "Fullname must be at least 2 characters").required("Fullname is required"),
  email: yup.string().email("Invalid email").required("Email is required"),
  password: yup.string().min(8, "Password must be at least 8 characters").required("Password is required"),
});

// Initialize VeeValidate form with schema
const { handleSubmit } = useForm({ validationSchema });

const fullname = useField("fullname");
const email = useField("email");
const password = useField("password");

// Handle form submission
const onSubmit = handleSubmit((values) => {
  console.log("User Registered:", values);
  alert(`Welcome ${values.fullname}, your account has been created.`);
  router.push("/"); // Redirect to homepage
});
</script>

<template>
  <div class="w-full min-h-[calc(100vh-10rem)] flex items-center justify-center bg-white">
    <div class="w-full text-black p-2 max-w-md flex justify-center flex-col gap-8">
      <h1 class="text-3xl">Create an account</h1>
      <form @submit.prevent="onSubmit" class="flex flex-col gap-5 items-center">
        
        <!-- Fullname Field -->
        <label for="fullname" class="w-full flex flex-col gap-2">
          <span class="text-sm">Fullname</span>
          <input
            v-model="fullname.value.value"
            class="w-full p-2 border-2 border-accent rounded-md"
            type="text"
            id="fullname"
          />
          <p class="text-red-500 text-sm" v-if="fullname.errorMessage">{{ fullname.errorMessage }}</p>
        </label>

        <!-- Email Field -->
        <label for="email" class="w-full flex flex-col gap-2">
          <span class="text-sm">Email</span>
          <input
            v-model="email.value.value"
            class="w-full p-2 border-2 border-accent rounded-md"
            type="email"
            id="email"
          />
          <p class="text-red-500 text-sm" v-if="email.errorMessage">{{ email.errorMessage }}</p>
        </label>

        <!-- Password Field -->
        <label for="password" class="w-full flex flex-col gap-2">
          <span class="text-sm">Password</span>
          <input
            v-model="password.value.value"
            class="w-full p-2 border-2 border-accent rounded-md"
            type="password"
            id="password"
          />
          <p class="text-red-500 text-sm" v-if="password.errorMessage">{{ password.errorMessage }}</p>
        </label>

        <!-- Submit Button -->
        <button
          type="submit"
          class="min-w-48 py-3 rounded-xl text-white px-2 bg-tertiary border-accent border-[1px]"
        >
          Create
        </button>
      </form>
    </div>
  </div>
</template>
