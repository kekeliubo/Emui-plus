## form

 <emui-form :model="activity" :rules="rules" ref="form">
        <emui-form-item label="活动名称" prop="name">
          <emui-input v-model="activity.name"></emui-input>
        </emui-form-item>
        <emui-form-item label="活动地点" prop="address">
          <emui-radio-group v-model="activity.address">
            <emui-radio label="上海"></emui-radio>
            <emui-radio label="北京"></emui-radio>
          </emui-radio-group>
        </emui-form-item>
        <emui-form-item label="活动方式" prop="way">
          <emui-radio-group v-model="activity.way">
            <emui-radio-button label="组队"></emui-radio-button>
            <emui-radio-button label="个人"></emui-radio-button>
          </emui-radio-group>
        </emui-form-item>
        <emui-form-item label="活动性质" prop="datalist">
          <emui-checkbox-group v-model="activity.datalist">
            <emui-checkbox label="品牌推广"></emui-checkbox>
            <emui-checkbox label="形象普及"></emui-checkbox>
          </emui-checkbox-group>
        </emui-form-item>
        <emui-form-item label="请选择" prop="myValue">
          <emui-select v-model="activity.myValue" placeholder="请选择">
            <emui-option
              v-for="item in options"
              :label="item.label"
              :value="item.key"
              :key="item.key"
            ></emui-option>
          </emui-select>
        </emui-form-item>
        <emui-form-item>
          <emui-button @click="handleSubmit">提交</emui-button>
          <emui-button @click="handleReset">重置</emui-button>
        </emui-form-item>
</emui-form>

<script lang="ts" setup>
import { reactive, ref } from 'vue'
let options = reactive([
  { key: 'key1', label: '选项1' },
  { key: 'key2', label: '选项2' },
  { key: 'key3', label: '选项3' },
  { key: 'key4', label: '选项4' },
  { key: 'key5', label: '选项5' },
  { key: 'key6', label: '选项6' },
  { key: 'key7', label: '选项7' }
])
let activity = reactive({
  datalist: [],
  name: '',
  address: '',
  way: '',
  myValue: ''
})
let rules = reactive({
  name: [{ required: true, message: '不能为空', trigger: 'blur' }],
  address: [{ required: true, message: '不能为空', trigger: 'change' }],
  way: [{ required: true, message: '不能为空', trigger: 'change' }],
  datalist: [
    {
      type: 'array',
      required: true,
      message: '不能为空',
      trigger: 'change'
    }
  ],
  myValue: [{ required: true, message: '至少选择一项' }]
})

const form = ref()
function handleSubmit() {
  form.value.validate((valid) => {
    if (valid) console.log('提交成功')
    else console.log('校验失败')
  })
}
function handleReset() {
  form.value.resetFields()
}
</script>