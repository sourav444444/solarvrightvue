<template>
  <section class="px-6 py-16 max-w-xl mx-auto">
    <h2 class="text-3xl font-bold text-green-700 mb-6">Enquiry Form</h2>
    <form @submit.prevent="handleSubmit" class="space-y-4">
      <div v-for="field in ['name', 'email', 'phone', 'message']" :key="field">
        <input
          v-model="form[field]"
          :type="field === 'email' ? 'email' : 'text'"
          :placeholder="field.charAt(0).toUpperCase() + field.slice(1)"
          class="w-full p-3 border border-slate-300 rounded-md focus:outline-none focus:ring-2 focus:ring-green-400"
          :rows="field === 'message' ? 4 : undefined"
        />
        <p v-if="errors[field]" class="text-red-500 text-sm">{{ errors[field] }}</p>
      </div>
      <button
        type="submit"
        class="bg-green-600 text-white px-6 py-3 rounded-full hover:bg-green-700 transition"
      >
        Submit
      </button>
    </form>
  </section>
</template>

<script setup>
import { reactive } from 'vue'

const form = reactive({ name: '', email: '', phone: '', message: '' })
const errors = reactive({})

function validate() {
  errors.name = form.name ? '' : 'Name is required'
  errors.email = /\S+@\S+\.\S+/.test(form.email) ? '' : 'Valid email is required'
  errors.phone = form.phone.length >= 10 ? '' : 'Valid phone number is required'
  errors.message = form.message ? '' : 'Message is required'

  return !errors.name && !errors.email && !errors.phone && !errors.message
}

function handleSubmit() {
  if (validate()) {
    alert('Form submitted successfully!')
    form.name = form.email = form.phone = form.message = ''
  }
}
</script>
