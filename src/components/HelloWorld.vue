<script setup lang="ts">
import { h, reactive, ref } from 'vue'
import { IconSearch } from '@arco-design/web-vue/es/icon'
import Table from '../components/Table.vue'

defineProps<{ msg: string }>()

const count = ref(0)
const columns = [
  {
    title: 'Name',
    dataIndex: 'name',
    type: 'select',
    search: true,
    filterable: {
      filter: (value, record) => record.name.includes(value),
      slotName: 'name-filter',
      icon: () => h(IconSearch),
    },
  },
  {
    title: 'Salary',
    dataIndex: 'salary',
    search: true,
    sortable: {
      sortDirections: ['ascend'],
    },
  },
  {
    title: 'Address',
    dataIndex: 'address',
  },
  {
    title: 'Email',
    dataIndex: 'email',
  },
]
const data = reactive([{
  key: '1',
  name: 'Jane Doe',
  salary: 23000,
  address: '32 Park Road, London',
  email: 'jane.doe@example.com',
}, {
  key: '2',
  name: 'Alisa Ross',
  salary: 25000,
  address: '35 Park Road, London',
  email: 'alisa.ross@example.com',
}, {
  key: '3',
  name: 'Kevin Sandra',
  salary: 22000,
  address: '31 Park Road, London',
  email: 'kevin.sandra@example.com',
}, {
  key: '4',
  name: 'Ed Hellen',
  salary: 17000,
  address: '42 Park Road, London',
  email: 'ed.hellen@example.com',
}, {
  key: '5',
  name: 'William Smith',
  salary: 27000,
  address: '62 Park Road, London',
  email: 'william.smith@example.com',
}])

function onLoad(query: {}) {
  console.log('query', query)
}
const reset = (data: {}) => {
  console.log('reset', data)
}
</script>

<template>
  <h1>{{ msg }}</h1>
  <div class="card">
    <a-button type="primary" @click="count++">
      count is {{ count }}
    </a-button>
    <p>
      Edit
      <code>components/HelloWorld.vue</code> to test HMR
    </p>
  </div>
  <Table :columns="columns" :data="data" @search="onLoad" @reset="reset" />
  <p>
    Check out
    <a href="https://vuejs.org/guide/quick-start.html#local" target="_blank">create-vue</a>, the official Vue + Vite
    starter
  </p>
  <p>
    Install
    <a href="https://github.com/johnsoncodehk/volar" target="_blank">Volar</a>
    in your IDE for a better DX
  </p>
  <p class="read-the-docs">
    Click on the Vite and Vue logos to learn more
  </p>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
