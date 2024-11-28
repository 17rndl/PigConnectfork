<template>
  <LoginLayout>
    <Head title="Register" />
    <div class="md:max-w-md w-full px-4 py-4">
      <form @submit.prevent="submit">
        <div class="mb-12">
          <h3 class="text-gray-800 text-3xl font-extrabold">Register</h3>
          <p class="text-sm mt-4 text-gray-800">Already have an account? 
            <a :href="route('login')" class="text-blue-600 font-semibold hover:underline ml-1 whitespace-nowrap">Log in here</a>
          </p>
        </div>

        <div>
          <label class="text-gray-800 text-xs block mb-2">Name</label>
          <TextInput name="name" type="text" v-model="form.name" required class="w-full text-gray-800 text-sm border-b border-[#C58A61] focus:border-[#C58A61] px-2 py-3 outline-none" placeholder="Enter name" />
          <InputError :message="form.errors.name" class="mt-2" />
        </div>

        <div class="mt-8">
          <label class="text-gray-800 text-xs block mb-2">Role</label>
          <select id="role" v-model="form.role" class="mt-1 block w-full text-gray-800 text-sm border-b border-[#C58A61] focus:border-[#C58A61] px-2 py-3 outline-none bg-white">
            <option value="farmer">Farmer</option>
            <option value="buyer">Buyer</option>
          </select>
          <InputError :message="form.errors.role" class="mt-2" />
        </div>

        <div class="mt-8">
          <label class="text-gray-800 text-xs block mb-2">Email</label>
          <div class="relative flex items-center">
            <TextInput name="email" type="email" v-model="form.email" required class="w-full text-gray-800 text-sm border-b border-[#C58A61] focus:border-[#C58A61] px-2 py-3 outline-none" placeholder="Enter email" />
            <svg xmlns="http://www.w3.org/2000/svg" fill="#C58A61" stroke="#C58A61" class="w-[18px] h-[18px] absolute right-2" viewBox="0 0 682.667 682.667">
              <defs>
                <clipPath id="a" clipPathUnits="userSpaceOnUse">
                  <path d="M0 512h512V0H0Z" data-original="#000000"></path>
                </clipPath>
              </defs>
              <g clip-path="url(#a)" transform="matrix(1.33 0 0 -1.33 0 682.667)">
                <path fill="none" stroke-miterlimit="10" stroke-width="40" d="M452 444H60c-22.091 0-40-17.909-40-40v-39.446l212.127-157.782c14.17-10.54 33.576-10.54 47.746 0L492 364.554V404c0 22.091-17.909 40-40 40Z" data-original="#000000"></path>
                <path d="M472 274.9V107.999c0-11.027-8.972-20-20-20H60c-11.028 0-20 8.973-20 20V274.9L0 304.652V107.999c0-33.084 26.916-60 60-60h392c33.084 0 60 26.916 60 60v196.653Z" data-original="#000000"></path>
              </g>
            </svg>
          </div>
          <InputError :message="form.errors.email" class="mt-2" />
        </div>

        <div class="mt-8">
          <label class="text-gray-800 text-xs block mb-2">Password</label>
          <div class="relative flex items-center">
            <TextInput :type="showPassword ? 'text' : 'password'" name="password" v-model="form.password" required class="w-full text-gray-800 text-sm border-b border-[#C58A61] focus:border-[#C58A61] px-2 py-3 outline-none" placeholder="Enter password" />
            <svg @click="togglePasswordVisibility" xmlns="http://www.w3.org/2000/svg" fill="#C58A61" stroke="#C58A61" class="w-[18px] h-[18px] absolute right-2 cursor-pointer" viewBox="0 0 128 128">
              <path d="M64 104C22.127 104 1.367 67.496.504 65.943a4 4 0 0 1 0-3.887C1.367 60.504 22.127 24 64 24s62.633 36.504 63.496 38.057a4 4 0 0 1 0 3.887C126.633 67.496 105.873 104 64 104zM8.707 63.994C13.465 71.205 32.146 96 64 96c31.955 0 50.553-24.775 55.293-31.994C114.535 56.795 95.854 32 64 32 32.045 32 13.447 56.775 8.707 63.994zM64 88c-13.234 0-24-10.766-24-24s10.766-24 24-24 24 10.766 24 24-10.766 24-24 24zm0-40c-8.822 0-16 7.178-16 16s7.178 16 16 16 16-7.178 16-16-7.178-16-16-16z" data-original="#000000"></path>
            </svg>
          </div>
          <InputError :message="form.errors.password" class="mt-2" />
        </div>

        <div class="mt-8">
          <label class="text-gray-800 text-xs block mb-2">Confirm Password</label>
          <TextInput name="password_confirmation" type="password" v-model="form.password_confirmation" required class="w-full text-gray-800 text-sm border-b border-[#C58A61] focus:border-[#C58A61] px-2 py-3 outline-none" placeholder="Confirm password" />
          <InputError :message="form.errors.password_confirmation" class="mt-2" />
        </div>

        <div class="mt-12">
          <PrimaryButton class="w-full shadow-xl py-2.5 px-4 text-sm tracking-wide rounded-md text-white bg-[#C58A61] hover:bg-[#C58A61] focus:outline-none" :disabled="form.processing">
            Register
          </PrimaryButton>
        </div>
      </form>
    </div>
  </LoginLayout>
</template>

<script setup>
import LoginLayout from '@/Layouts/LoginLayout.vue';
import InputError from '@/Components/InputError.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import { Head, useForm } from '@inertiajs/vue3';
import { ref } from 'vue';

const form = useForm({
  name: '',
  role: '',
  email: '',
  password: '',
  password_confirmation: '',
});

const showPassword = ref(false);

const togglePasswordVisibility = () => {
  showPassword.value = !showPassword.value;
};

const submit = () => {
  form.post(route('register'), {
    onFinish: () => form.reset('password', 'password_confirmation'),
  });
};
</script>