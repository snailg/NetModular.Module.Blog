<template>
  <nm-container>
    <nm-list ref="list" v-bind="list">
      <!--查询条件-->
      <template v-slot:querybar>
        <el-form-item label="文章编号：" prop="articleId">
          <el-input v-model="list.model.articleId" clearable/>
        </el-form-item>
        <el-form-item label="标签编号：" prop="tagId">
          <el-input v-model="list.model.tagId" clearable/>
        </el-form-item>
      </template>

      <!--按钮-->
      <template v-slot:querybar-buttons>
        <nm-button-has :options="buttons.add" @click="add" />
      </template>

      <!--自定义列-->
      <!-- <template v-slot:col-name="{row}">
        <nm-button :text="row.name" type="text" />
      </template> -->

      <!--操作列-->
      <template v-slot:col-operation="{row}">
        <nm-button v-bind="buttons.edit" @click="edit(row)" />
        <nm-button-delete v-bind="buttons.del" :id="row.id" :action="removeAction" @success="refresh"/>
      </template>
    </nm-list>

    <!--添加-->
    <add-page :visible.sync="dialog.add" @success="refresh"/>
    <!--编辑-->
    <edit-page :id="curr.id" :visible.sync="dialog.edit" @success="refresh"/>
  </nm-container>
</template>
<script>
import page from './page'
import cols from './cols'
import AddPage from '../components/add'
import EditPage from '../components/edit'

const api = $api.blog.articleTag

export default {
  name: page.name,
  components: { AddPage, EditPage },
  data () {
    return {
      curr: { id: '' },
      list: {
        title: page.title,
        cols,
        action: api.query,
        model: {
          /** 文章编号 */
          articleId: '',
          /** 标签编号 */
          tagId: ''
        }
      },
      removeAction: api.remove,
      dialog: {
        add: false,
        edit: false
      },
      buttons: page.buttons
    }
  },
  methods: {
    refresh () {
      this.$refs.list.refresh()
    },
    add () {
      this.dialog.add = true
    },
    edit (row) {
      this.curr = row
      this.dialog.edit = true
    }
  }
}
</script>
