<template>
    <div>
      <h2>Lista de Contactos</h2>
      <table>
        <thead>
          <tr>
            <th>Nombre</th>
            <th>Correo</th>
            <th>Dirección</th>
            <th>Teléfono</th>
            <th>País</th>
            <th>Ciudad</th>
            <th>Acciones</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="contact in contacts" :key="contact.id">
            <td>{{ contact.name }}</td>
            <td>{{ contact.email }}</td>
            <td>{{ contact.address }}</td>
            <td>{{ contact.phone }}</td>
            <td>{{ contact.country }}</td>
            <td>{{ contact.city }}</td>
            <td>
              <button @click="$emit('onEdit', contact)">Editar</button>
              <button @click="deleteContact(contact)">Eliminar</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      contacts: Array,
    },
    methods: {

    editContact(contact) {
      // Emit an event to the parent component with the contact to be edited
      this.$emit('onEdit', contact);
    },
      deleteContact(contact) {
        if(confirm("Estas seguro de eliminar este contacto")) {
          this.$emit('deleteContact', contact.id);
          // Remove the contact from the contacts array and
          const index = this.contacts.indexOf(contact);
          if (index > -1) {
            this.contacts.splice(index, 1);
          }
        }
      }
    }
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