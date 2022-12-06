<script setup>
import { ref } from 'vue'
import SimpleTable from './SimpleTable.vue';

const items = ref([
  { id: 1, name: "Hola", isActive: true },
  { id: 2, name: "BHola", isActive: false },
  { id: 3, name: "SHola", isActive: true },
]);
  
const columns = ref([
  { header: "Id", name:"id"},
  { header: "Name", name:"name" },
  { header: "Status", name:"status", displayField: "isActive" },
  { header: "Action", name:"action" },
]);

</script>

<template>
  <SimpleTable :data="items" :column-defs="columns">
    <template #col.status="{ item }">
      <span v-if="item.isActive">
      	<input type="checkbox" checked disabled/>
      </span>
      <span v-else>
      	<input type="checkbox" disabled/>
      </span>
    </template>
  </SimpleTable>
</template>