<template>
    <table>
        <thead>
          <tr>
            <th v-for="column in columnDefs">
              {{column.header}}
          </th>
        </tr>
      </thead>
      <tbody>
          <tr v-for="item in data">
            <td v-for="column in columnDefs">
              <slot :name="`col.${column.name}`" :item="item">
              <template v-if="column.displayField">
                  {{item[column.displayField]}}
              </template>
              <template v-else="column.displayField">
                  {{item[column.name]}}
              </template>
            </slot>
          </td>
        </tr>
      </tbody>
    </table>
    </template>
    
    <script setup>
    const props = defineProps({
      data: Array,
      columnDefs: Array
    });
    </script>
    
    <style>
      table {
        width: 100%;
        color: gray;
        border-collapse: collapse;
      }
      td,th {
        text-align: left;
        border: 1px solid black;
        padding: 10px;
      }
    </style>