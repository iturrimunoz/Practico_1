<template>
    <div>
      <h2>Filtrar Contactos</h2>
      <input v-model="filter.name" placeholder="Nombre" />
      <input v-model="filter.email" placeholder="Correo" />
      <button @click="applyFilter">Filtrar</button>
    </div>
  </template>
  
  <script>
  import { reactive } from 'vue';
  
  export default {
    props: {
      onFilter: Function,
    },
    setup(props) {
      const filter = reactive({ name: '', email: '' });
  
      const applyFilter = () => {
        props.onFilter({ ...filter });
      };
  
      return { filter, applyFilter };
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