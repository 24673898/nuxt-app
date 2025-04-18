<template>
  <div class="contact-container">
    <h1>Contact Me</h1>
    
    <form
      name="contact"
      method="POST"
      data-netlify="true"
      data-netlify-honeypot="bot-field"
      class="contact-form"
      @submit.prevent="handleSubmit"
    >
      <input type="hidden" name="form-name" value="contact">
      <input type="hidden" name="bot-field">
      
      <div class="form-group">
        <label for="name">Your Name</label>
        <input
          type="text"
          id="name"
          name="name"
          v-model="formData.name"
          required
          placeholder="John Doe"
        >
      </div>
      
      <div class="form-group">
        <label for="email">Your Email</label>
        <input
          type="email"
          id="email"
          name="email"
          v-model="formData.email"
          required
          placeholder="your@email.com"
        >
      </div>
      
      <div class="form-group">
        <label for="message">Your Message</label>
        <textarea
          id="message"
          name="message"
          v-model="formData.message"
          rows="5"
          required
          placeholder="Your message here..."
        ></textarea>
      </div>
      
      <button type="submit" class="submit-button">
        Send Message
      </button>
      
      <div v-if="formStatus" class="status-message" :class="statusClass">
        {{ formStatus }}
      </div>
    </form>
  </div>
</template>

<script setup>
const formData = reactive({
  name: '',
  email: '',
  message: ''
});

const formStatus = ref('');
const statusClass = ref('');

const handleSubmit = async () => {
  try {
    const formPayload = new FormData();
    formPayload.append('form-name', 'contact');
    Object.entries(formData).forEach(([key, value]) => {
      formPayload.append(key, value);
    });

    await fetch('/', {
      method: 'POST',
      headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
      body: new URLSearchParams(formPayload).toString()
    });

    formStatus.value = 'Message sent successfully!';
    statusClass.value = 'success';
    
    formData.name = '';
    formData.email = '';
    formData.message = '';
    
    setTimeout(() => {
      formStatus.value = '';
    }, 5000);

  } catch (error) {
    formStatus.value = 'Failed to send message. Please try again.';
    statusClass.value = 'error';
    console.error('Form submission error:', error);
  }
};
</script>

<style>
.contact-container {
  max-width: 800px;
  margin: 0 auto;
  padding: 2rem 1rem;
}

.contact-container h1 {
  font-size: 2rem;
  color: #333;
  margin-bottom: 1.5rem;
  text-align: center;
}

.contact-form {
  background-color: white;
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.form-group {
  margin-bottom: 1.5rem;
}

.form-group label {
  display: block;
  font-size: 0.9rem;
  color: #444;
  margin-bottom: 0.5rem;
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 0.75rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 1rem;
}

.form-group textarea {
  min-height: 150px;
  resize: vertical;
}

.submit-button {
  width: 100%;
  padding: 0.75rem;
  background-color: #0066cc;
  color: white;
  border: none;
  border-radius: 4px;
  font-size: 1rem;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.submit-button:hover {
  background-color: #0052a3;
}

.status-message {
  margin-top: 1rem;
  padding: 0.75rem;
  border-radius: 4px;
}

.status-message.success {
  background-color: #e6ffed;
  color: #22863a;
}

.status-message.error {
  background-color: #ffeef0;
  color: #cb2431;
}
</style>