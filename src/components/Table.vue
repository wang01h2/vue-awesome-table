<script setup lang="ts">
import { reactive } from 'vue'

interface Props {
  columns: any[]
  data: any[]
}

const props = defineProps<Props>()
defineEmits(['search'])
const tableData = reactive({ form: {}, searchColumns: [] as any[] })
/*
* 封装思想
*
* */
const handleChange = (data: any[], extra: any) => {
  console.log('change', data, extra)
}
const form = props.columns.filter(item => item.search).map(item => item.dataIndex).reduce((arr, item, index) => {
  arr[item] = ''
  return arr
}, {})
tableData.form = form
tableData.searchColumns = props.columns.filter(item => item.search)
console.log('form', form)
</script>

<template>
  <a-card :style="{ width: '100%' }" :bordered="false">
    <a-form ref="formRef" :model="tableData.form">
      <a-row :gutter="16">
        <a-col v-for="(item, index) in tableData.searchColumns" :key="index" :span="8">
          <a-form-item field="value1" :label="item.title" label-col-flex="100px">
            <a-input v-if="item.type === 'input' || !item.type" v-model="tableData.form[item.dataIndex]" placeholder="please enter..." />
            <a-select v-if="item.type === 'select'" v-model="tableData.form[item.dataIndex]" :style="{ width: '320px' }" placeholder="Please select ..." allow-clear>
              <a-option v-for="(item2, index2) in data" :key="index2">
                {{ item2.name }}
              </a-option>
            </a-select>
          </a-form-item>
        </a-col>
        <a-col :span="8">
          <a-form-item>
            <a-space>
              <a-button html-type="submit" @click="$emit('search', tableData.form)">
                Search
              </a-button>
              <a-button @click="$refs.formRef.resetFields()">
                Reset
              </a-button>
            </a-space>
          </a-form-item>
        </a-col>
      </a-row>
      <a-table :columns="columns" :data="data" @change="handleChange">
        <template #name-filter="{ filterValue, setFilterValue, handleFilterConfirm, handleFilterReset }">
          <div class="custom-filter">
            <a-space direction="vertical">
              <a-input :model-value="filterValue[0]" @input="(value) => setFilterValue([value])" />
              <div class="custom-filter-footer">
                <a-button @click="handleFilterConfirm">
                  Confirm
                </a-button>
                <a-button @click="handleFilterReset">
                  Reset
                </a-button>
              </div>
            </a-space>
          </div>
        </template>
      </a-table>
    </a-form>
  </a-card>
</template>

<style scoped>
.custom-filter {
  padding: 20px;
  background: var(--color-bg-5);
  border: 1px solid var(--color-neutral-3);
  border-radius: var(--border-radius-medium);
  box-shadow: 0 2px 5px rgb(0 0 0 / 10%);
}

.custom-filter-footer {
  display: flex;
  justify-content: space-between;
}
</style>
