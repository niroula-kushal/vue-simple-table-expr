### Vue Simple Table

An experimental vue implementation for tables that intends to make building dynamic tables easier.

### Desired Usage

1. User should be able to provide data in an array format. Individual data can be in the format they choose.
2. User should be able to provide column definitions. Column definitions should contain basic information like the name of the column, the header display value and the field to display by default.
3. If the user desires, the user should be able to customize the way a data or column is rendered.

### Experimental API Usage

For point #3, we need to provide an api that is both flexible and easy to use.

We can use a render function to deliver that, however the DX of using render function is not so great as the templating eventhough it opens up the full power of javascript.

Another option is to use render function with JSX, however that requires the project to have JSX setup.

We have decided to leverage the power of slots to power our api.

Vue has the concept of slots that allows a parent to pass in templating data to its children. The neat thing about this is that slots can be dynamic.

In our implementation, we are renderin each data in our table in their own `td` or `cell`. During render, we also render a dynamic slot with the name of the column. The format of the slot name is `col.${columnName}`. We also provide the row item as a slot props `item`.

This allows the caller to specify how to display a specific column data using the above notation.

### Example

Consider the following column definitions.

```vue

<script setup>

const items = ref([
    // data 
]);

const columns = ref([
  { header: "Id", name:"id"},
  { header: "Name", name:"name" },
  { header: "Status", name:"status", displayField: "isActive" },
  { header: "Action", name:"action" },
]);

</script>

...

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

```

We are customizing the appearance of the status column. In order to do that we are providing the template in the "col.status" slot. If we wanted to customize our "action" column, we would use the slot "col.action".


## Demo

https://vue-simple-table-expr.netlify.app/
