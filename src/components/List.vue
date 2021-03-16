<template>
  <el-dialog
    :visible="visible"
    @close="$emit('update:visible', false)"
    width="700px"
    height="100%"
    class="c-List"
    :append-to-body="true"
  >
    <div>
      <div class="dialog-title" slot="title">
        <span :style="{ fontSize: '18px' }">
          名单
        </span>
      </div>
      <el-table :data="tableData" stripe height="800px" style="width: 100%">
        <el-table-column prop="key" label="抽奖号码" width="130" />
        <el-table-column prop="name" label="名字" />
        <el-table-column prop="block" label="Block" width="100">
          <template slot-scope="scope">
            <el-checkbox v-model="tableData[scope.$index].block" />
          </template>
        </el-table-column>
        <el-table-column width="100" label="删除">
          <template slot-scope="scope">
            <el-button
              @click.native.prevent="deleteRow(scope.$index, tableData)"
              type="text"
              size="small"
            >
              删除
            </el-button>
          </template>
        </el-table-column>
      </el-table>
    </div>
    <el-button type="primary" @click="saveList">确定保存</el-button>
  </el-dialog>
</template>

<script>
export default {
  name: 'c-List',
  props: {
    visible: Boolean
  },
  data() {
    return {
      tableData: this.$store.state.list
    };
  },
  methods: {
    deleteRow(index, rows) {
      rows.splice(index, 1);
    },
    saveList() {
      const { tableData } = this;
      this.$store.commit('setList', tableData);
      this.$message({
        message: '保存成功',
        type: 'success'
      });
    }
  }
};
</script>

<style lang="scss">
.c-List {
  .el-dialog__body {
    max-height: 60vh;
    overflow-y: auto;
  }
}
</style>
