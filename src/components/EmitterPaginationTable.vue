<template>
  <div>
    <el-table
      :data="dataAfterFilter"
      stripe
      size="small"
      border
      min-height=300
      >
      <el-table-column
        type="index"
        :index="idIndex"
        label="ID"
        sortable
        width="150"
        >
      </el-table-column>

      <slot name="default"></slot>

      <el-table-column label="Operation">
        <template slot="header" slot-scope="scope">
          <input
            class="el-input__inner key-detail-filter-value"
            v-model="filterValue"
            :placeholder="$t('message.key_to_search')"
            />
        </template>
        <template slot-scope="scope">
          <el-button type="text" @click="$parent.showEditDialog(scope.row)" icon="el-icon-edit" circle>
          </el-button>
          <el-button type="text" @click="$parent.deleteLine(scope.row)" icon="el-icon-delete" circle>
          </el-button>
        </template>
      </el-table-column>
    </el-table>

    <el-pagination
      class="pagenation-table-page-container"
      :total="dataTotal"
      :page-size="pageSize"
      :current-page.sync="pageIndex"
      layout="prev, pager, next"
      background
      >
    </el-pagination>
  </div>
</template>

<script type="text/javascript">
export default {
  data() {
    return {
      pageIndex: 1,
      filterValue: '',
    };
  },
  props: ['data', 'filterKey', 'dataTotal', 'pageSize'],
  watch: {
    pageIndex(pageIndex) {
      this.$parent.changePageIndex(pageIndex);
    },
  },
  computed: {
    dataAfterFilter() {
      const filterKey = this.filterKey;
      const filterValue = this.filterValue;

      if (!filterValue || !filterKey) {
        return this.data;
      }

      return this.data.filter(line => line[filterKey].toLowerCase().includes(filterValue.toLowerCase()));
    },
  },
  methods: {
    idIndex(index) {
      return (this.pageIndex - 1) * this.pageSize + index + 1;
    },
  },
};
</script>

<style type="text/css">
  .pagenation-table-page-container {
    margin-top: 20px;
  }
</style>
