<template>
  <el-form>
    <el-form-item>
      <el-input type="textarea" size="small" rows="12" :value="newContent"></el-input>
    </el-form-item>
  </el-form>
</template>

<script>
export default {
  data() {
    return {};
  },
  props: ['data', 'redisKey'],
  computed: {
    newContent() {
      return this.$util.hexAddX(this.data.contentBuffer.toString('hex'));
    },
  },
};
</script>
