<template>
  <nm-form-dialog ref="form" v-bind="form" v-on="on" :visible.sync="visible_">
    <el-row>
      <el-col :span="20" :offset="1">
        <el-form-item label="名称：" prop="name">
          <el-input v-model="form.model.name" clearable/>
        </el-form-item>
        <el-form-item label="编码：" prop="code">
          <el-input v-model="form.model.code" clearable/>
        </el-form-item>
        <el-form-item label="文章数量：" prop="count">
          <el-input v-model="form.model.count" clearable/>
        </el-form-item>
      </el-col>
    </el-row>
  </nm-form-dialog>
</template>
<script>
import { mixins } from 'netmodular-ui'

const api = $api.blog.category

export default {
  mixins: [mixins.formDialogEdit],
  data () {
    return {
      api,
      form: {
        title: '编辑分类',
        action: api.update,
        model: {
          /** 名称 */
          name: '',
          /** 编码 */
          code: '',
          /** 文章数量 */
          count: ''
        },
        rules: {
        }
      }
    }
  }
}
</script>
