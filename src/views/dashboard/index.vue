<template>
    <div class="dashboard-container">
        <el-button type="text" @click="add">当前编号：{{currentNumber}}</el-button>
    </div>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  name: 'Dashboard',
  computed: {
    ...mapGetters([
      'name'
    ])
  },
  data() {
      return {
          currentNumber: 1
      }
  },
  methods: {
      add() {
            let fileContent =  '编号\n';
            for(let i = 0; i <= this.currentNumber; i++) {
                fileContent += i + '\n';
            }
            let fileName = '编号.csv';
            let uriContent = URL.createObjectURL(new Blob([fileContent], {type: 'text/plain'}));
            let link = document.createElement('a');
            link.setAttribute('href', uriContent);
            link.setAttribute('download', fileName);
            let event = new MouseEvent('click');
            link.dispatchEvent(event);
            this.$message.success('编号导出成功');
            this.currentNumber++;
      }
  }
}
</script>

<style lang="scss" scoped>
.dashboard {
  &-container {
    margin: 30px;
  }
  &-text {
    font-size: 30px;
    line-height: 46px;
  }
}
</style>
