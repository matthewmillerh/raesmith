<script setup>
import emailjs from '@emailjs/browser';
import { ref } from 'vue';

const form = ref(null);
const inputFieldReset = ref(null);

const sendMail = () => {
    emailjs.sendForm('service_qg7afqq', 'template_yrm6lm8', form.value, 'RyIXXr7-ppm95PWre')
    .then(() => {
        alert('Message sent!')
        inputFieldReset.value = " ";
    }, (error) => {
        alert('Message not sent', error);
    }); 
    }
</script>

<template>
    <form class="form" ref="form" @submit.prevent="sendMail">
        <div class="md:w-1/3 lg:w-1/3 sm:w-10/12 w-10/12 ml-auto mr-auto mt-14 text-justify">
            <p class="mb-5"><input type="text" placeholder=" Name" name="from_name" :value="inputFieldReset" class="rounded border border-gray-400 w-full" required/></p>
            <p class="mb-5"><input type="email" placeholder=" Email" name="email" :value="inputFieldReset" class="rounded border border-gray-400 w-full" required/></p>
            <p class="mb-5"><textarea placeholder=" Message" name="message" :value="inputFieldReset" class="rounded border border-gray-400 w-full h-60" required></textarea></p>
            <button type="submit" name="send" class="border border-gray-100 bg-gray-50 rounded p-2">Submit</button>
        </div>
    </form>
    
</template>

<style>
</style>