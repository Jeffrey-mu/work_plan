<script lang="ts" setup>
const data_info = ref([
  `${ new Date().getMonth() + 1 + '.'+ new Date().getDate()}工作计划`,
  '亚马逊账号日常维护',
  'dv优化，上素材和订单项',
  '亚马逊账号日常维护'
])
function copyText() {
  window.navigator.clipboard.writeText(data_info.value.map((item, index) =>
    index ? index + '、' + item : item
  ).join('\n')).then((_res) => {
    localStorage.setItem('data_info', JSON.stringify(data_info.value))
  })
}
function handleAdd() {
  data_info.value.push('')
}
function isTrue() {
  return localStorage.getItem('data_info')
}
function handleDel(index) {
  data_info.value.splice(index, 1)
}
onMounted(() => {
  if (isTrue())
  data_info.value = JSON.parse(localStorage.getItem('data_info'))
  data_info.value[0] = `${new Date().getMonth() + 1 + '.' + new Date().getDate()}工作计划`
})
</script>
<template>
<div w-100 ma text-left class="box">
<div v-for="item,index in data_info" >
  {{ index ? index + '、' : ''}}{{ item }}
</div>
<hr my-2>
<h2>编辑区域</h2>
<template v-for="item, index in data_info">
  <div v-if="index" >
    {{ index }}、<input mt-3 b p-1 type="text" v-model="data_info[index]">
    <button btn mx-2 @click="handleDel(index)">del</button>
  </div>
</template>

<div>
  <button btn @click="copyText" m-2>copy</button>
  <button btn @click="handleAdd">add</button>
</div>
</div>
</template>
<style>
@media screen and (max-width: 900px) {
  .box {
    width: 100%;
  }
}
</style>
