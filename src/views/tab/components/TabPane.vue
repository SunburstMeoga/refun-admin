<template>
  <el-table :data="list" border fit highlight-current-row style="width: 100%">
    <el-table-column v-loading="loading" align="center" label="ID" width="65" element-loading-text="请给我点时间！">
      <template slot-scope="scope">
        <span>{{ scope.row.id }}</span>
      </template>
    </el-table-column>
    <el-table-column label="商品名称" align="center">
      <template slot-scope="{row}">
        <span>苹果 20W USB-C 电源适配器</span>
        <!-- <el-tag>{{ row.type }}</el-tag> -->
      </template>
    </el-table-column>
    <el-table-column width="180px" align="center" label="订单生成时间">
      <template slot-scope="scope">
        <span>{{ scope.row.timestamp | parseTime('{y}-{m}-{d} {h}:{i}') }}</span>
      </template>
    </el-table-column>

    <el-table-column label="商品配送地址" align="center">
      <template slot-scope="{row}">
        <span>广东省广州市荔湾区芳村3栋2323</span>
        <!-- <el-tag>{{ row.type }}</el-tag> -->
      </template>
    </el-table-column>

    <el-table-column align="center" label="商品数量">
      <template slot-scope="scope">
        <span>1</span>
      </template>
    </el-table-column>

    <el-table-column label="实际付款金额">
      <template slot-scope="scope">
        <span>232.2323 USDT</span>
      </template>
    </el-table-column>

    <el-table-column align="center" label="商品店铺名称">
      <template slot-scope="scope">
        <span>图拉斯旗舰店</span>
      </template>
    </el-table-column>
    <el-table-column align="center" label="共返利">
      <template slot-scope="scope">
        <span>232.2323 USDT</span>
      </template>
    </el-table-column>
    <el-table-column align="center" label="已返利">
      <template slot-scope="scope">
        <span>232.2323 USDT</span>
      </template>
    </el-table-column>
    <el-table-column align="center" label="剩余返利">
      <template slot-scope="scope">
        <span>232.2323 USDT</span>
      </template>
    </el-table-column>
    <!-- <el-table-column class-name="status-col" label="Status" width="110">
      <template slot-scope="{row}">
        <el-tag :type="row.status | statusFilter">
          {{ row.status }}
        </el-tag>
      </template>
    </el-table-column> -->
  </el-table>
</template>

<script>
import { fetchList } from '@/api/article'

export default {
  filters: {
    statusFilter(status) {
      const statusMap = {
        published: 'success',
        draft: 'info',
        deleted: 'danger'
      }
      return statusMap[status]
    }
  },
  props: {
    type: {
      type: String,
      default: 'CN'
    }
  },
  data() {
    return {
      list: null,
      listQuery: {
        page: 1,
        limit: 5,
        type: this.type,
        sort: '+id'
      },
      loading: false
    }
  },
  created() {
    this.getList()
  },
  methods: {
    getList() {
      this.loading = true
      this.$emit('create') // for test
      fetchList(this.listQuery).then(response => {
        this.list = response.data.items
        this.loading = false
      })
    }
  }
}
</script>
