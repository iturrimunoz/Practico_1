<template>
  <div id="app">
    <h1>Gestor de Contactos</h1>
    <ContactFilter :onFilter="filterContacts" />
    <ContactForm :onSave="saveContact" />
    <ContactList
      :contacts="filteredContacts"
      :onEdit="editContact"
      :onDelete="deleteContact"
    />
  </div>
</template>

<script>
import { ref } from 'vue';
import ContactList from './components/ContactList.vue';
import ContactForm from './components/ContactForm.vue';
import ContactFilter from './components/ContactFilter.vue';

export default {
  components: { ContactList, ContactForm, ContactFilter },
  setup() {
    const contacts = ref([]);
    const filteredContacts = ref([]);
    const filter = ref({ name: '', email: '' });

    const saveContact = (contact) => {
      if (contact.id) {
        const index = contacts.value.findIndex((c) => c.id === contact.id);
        contacts.value[index] = contact;
      } else {
        contact.id = Date.now();
        contacts.value.push(contact);
      }
      filteredContacts.value = [...contacts.value];
    };

    const deleteContact = (id) => {
      contacts.value = contacts.value.filter((c) => c.id !== id);
      filteredContacts.value = [...contacts.value];
    };

    const editContact = (contact) => {
      return contact;
    };

    const filterContacts = (criteria) => {
      filter.value = criteria;
      filteredContacts.value = contacts.value.filter(
        (c) =>
          (!criteria.name || c.name.includes(criteria.name)) &&
          (!criteria.email || c.email.includes(criteria.email))
      );
    };

    return {
      contacts,
      filteredContacts,
      saveContact,
      deleteContact,
      editContact,
      filterContacts,
    };
  },
};
</script>
