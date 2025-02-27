<script setup>
import { useForm, useField } from "vee-validate";
import * as yup from "yup";
import { useRouter } from "#app";

// Initialize Nuxt Router
const router = useRouter();

// Define validation schema using Yup
const validationSchema = yup.object({
  email: yup.string().email("Invalid email").required("Email is required"),
  password: yup.string().min(6, "Password must be at least 6 characters").required("Password is required"),
});

// Initialize VeeValidate form with schema
const { handleSubmit } = useForm({ validationSchema });

const email = useField("email");
const password = useField("password");

// Handle form submission
const onSubmit = handleSubmit((values) => {
  // Simulated login logic (replace with real authentication)
  if (values.email === "/login" && values.password === "password123") {
    alert(`Welcome back, ${values.email}`);
    router.push("/"); // Redirect to homepage
  } else {
    alert("Invalid email or password");
  }
});
</script>

<template>
  <div class="w-full min-h-[calc(100vh-10rem)] flex items-center justify-center bg-white">
    <div class="w-full text-black p-2 max-w-md flex justify-center flex-col gap-3">
      <h1 class="text-3xl">Welcome back,</h1>
      <p>
        Hi, my name is Eventful Moments. I am a bucket… no, not the bucket of
        water, but I store awesome moments you will like to have in coming years.
      </p>
      <form @submit.prevent="onSubmit" class="flex flex-col gap-5 items-center">
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
          Login
        </button>
      </form>
    </div>
  </div>
</template>
