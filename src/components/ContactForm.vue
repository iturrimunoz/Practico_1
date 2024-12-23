<template>
    <div>
      <h2>{{ contact.id ? 'Editar' : 'Agregar' }} Contacto</h2>
      <form @submit.prevent="submitForm">
        <input v-model="contact.name" placeholder="Nombre" required />
        <input v-model="contact.email" placeholder="Correo" required />
        <input v-model="contact.address" placeholder="Dirección" />
        <input v-model="contact.phone" placeholder="Teléfono" />
        <input v-model="contact.country" placeholder="País" />
        <input v-model="contact.city" placeholder="Ciudad" />
        <button type="submit">{{ contact.id ? 'Guardar' : 'Agregar' }}</button>
      </form>
    </div>
  </template>
  
  <script>
  import { reactive, watch } from 'vue';
  
  export default {
    props: {
      onSave: Function,
    },
    setup(props) {
      const contact = reactive({
        id: null,
        name: '',
        email: '',
        address: '',
        phone: '',
        country: '',
        city: '',
      });
  
      const submitForm = () => {
        props.onSave({ ...contact });
        Object.assign(contact, { id: null, name: '', email: '', address: '', phone: '', country: '', city: '' });
      };
  
      return { contact, submitForm };
    },
  };
  </script>
  <style scoped>
  table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 20px;
  }
  
  th, td {
    border: 1px solid #ddd;
    padding: 12px;
    text-align: left;
  }
  
  th {
    background-color: #f2f2f2;
    font-weight: bold;
  }
  
  tr:nth-child(even) {
    background-color: #f9f9f9;
  }
  
  tr:hover {
    background-color: #f5f5f5;
  }
  
  button {
    margin: 0 5px;
    padding: 5px 10px;
    background-color: #4CAF50;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  
  button:hover {
    background-color: #45a049;
  }
  
  button:last-child {
    background-color: #f44336;
  }
  
  button:last-child:hover {
    background-color: #d32f2f;
  }
  </style>