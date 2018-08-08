<template>
  <div>
    <el-row>
      <el-col :span="22" :offset="1">
        <h1>列合并dome</h1>
        <el-table
          :data="tableData"
          :span-method="objectSpanMethod"
          border
          style="width: 100%">
          <el-table-column
            label="地区"
            prop="address"
            fixed
            al
            width="300">
          </el-table-column>
          <el-table-column
            label="性别"
            prop="sex"
            width="300">
          </el-table-column>
          <el-table-column
            label="年龄"
            prop="age"
            width="350">
          </el-table-column>
          <el-table-column
            label="一"
            prop="one"
            width="300">
          </el-table-column>
          <el-table-column
            label="二"
            prop="two"
            width="300">
          </el-table-column>
          <el-table-column
            label="操作"
            fixed="right"
            width="300">
          <template slot-scope="scope">
            <el-button type="text" @click="add(scope.row)">添加</el-button>
            <el-button type="text" @click="update(scope.row)">编辑</el-button>
            <el-dropdown v-if="scope.row.num===3">
              <span class="el-dropdown-link">
                更多<i class="el-icon-arrow-down el-icon--right"></i>
              </span>
              <el-dropdown-menu slot="dropdown">
                <el-dropdown-item @click.native="show(scope.row)">查看</el-dropdown-item>
                <el-dropdown-item @click.native="del(scope.row)">删除</el-dropdown-item>
              </el-dropdown-menu>
            </el-dropdown>
          </template>
          </el-table-column>
        </el-table>
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {
  name: '',

  components: {

  },

  data () {
    return {
      tableData: [
        {
          one: '一',
          two: '二',
          name: '三',
          age: '18',
          sex: 'true',
          address: '北京',
          num: 1
        },
        {
          one: '一',
          two: '二',
          name: '三',
          age: '18',
          sex: 'true',
          address: '北京',
          num: 2
        },
        {
          one: '一',
          two: '二',
          name: '三',
          age: '18',
          sex: 'false',
          address: '北京',
          num: 2
        },
        {
          one: '一',
          two: '二',
          name: '三',
          age: '18',
          sex: 'false',
          address: '北京',
          num: 3
        },
        {
          one: '一',
          two: '二',
          name: '三',
          age: '18',
          sex: 'true',
          address: '上海',
          num: 1
        },
        {
          one: '一',
          two: '二',
          name: '三',
          age: '18',
          sex: 'true',
          address: '上海',
          num: 2
        },
        {
          one: '一',
          two: '二',
          name: '三',
          age: '18',
          sex: 'false',
          address: '上海',
          num: 3
        },
        {
          one: '一',
          two: '二',
          name: '三',
          age: '18',
          sex: 'false',
          address: '北京',
          num: 1
        },
        {
          one: '一',
          two: '二',
          name: '三',
          age: '18',
          sex: 'true',
          address: '北京',
          num: 2
        },
        {
          one: '一',
          two: '二',
          name: '三',
          age: '18',
          sex: 'true',
          address: '北京',
          num: 3
        }
      ],
      addressRowSpan: 0
    }
  },

  watch: {
  },

  mounted () {
  },

  methods: {
    objectSpanMethod ({ row, column, rowIndex, columnIndex }) {
      let addressSpanArr = []// 存放address需合并数据
      let addressSpanArrIndex = 0// address数据索引
      let sexSpanArr = []// 存放sex需合并数据
      let sexSpanArrIndex = 0// sex数据索引
      let _this = this

      this.tableData.forEach((item, index) => {
        if (index === 0) {
          addressSpanArr.push(1)
          sexSpanArr.push(1)
        } else {
          if (item.address === _this.tableData[index - 1].address) {
            addressSpanArr[addressSpanArrIndex] += 1
            addressSpanArr.push(0)
          } else {
            addressSpanArr.push(1)
            addressSpanArrIndex = index
          }
          if (item.sex === _this.tableData[index - 1].sex && item.address === _this.tableData[index - 1].address) {
            sexSpanArr[sexSpanArrIndex] += 1
            sexSpanArr.push(0)
          } else {
            sexSpanArr.push(1)
            sexSpanArrIndex = index
          }
        }
      })
      // 以上内容为对于table表单数据进行循环处理，表单合并所需数据进行存储
      // 此处操作会对页面性能产生影响,应写成单独方法,在通过API请求获取到数据之后调用此操作数据方法
      // dome数据为data中初始化数据并非动态数据因此临时写在此处
      if (column.property === 'address') {
        const addressRow = addressSpanArr[rowIndex]
        const addressCol = addressRow > 0 ? 1 : 0
        return {
          rowspan: addressRow,
          colspan: addressCol
        }
      }
      if (column.property === 'sex') {
        const sexRow = sexSpanArr[rowIndex]
        const sexCol = sexRow > 0 ? 1 : 0
        return {
          rowspan: sexRow,
          colspan: sexCol
        }
      }
    },
    add (row) {
      this.$message.info('您点击了添加按钮')
      console.log(row)
    },
    update (row) {
      this.$message.info('您点击率编辑按钮')
      console.log(row)
    },
    show (row) {
      this.$message.info('您点击了查看按钮')
      console.log(row)
    },
    del (row) {
      this.$message.info('您点击了删除安娜')
      console.log(row)
    },
    // 指令与事件只可用其一
    handleCommand (command) {
      if (command === 'show') {
        this.$message.info('查看指令' + command)
      }
      if (command === 'delete') {
        this.$message.info('删除指令' + command)
      }
    }
  }
}
</script>

<style lang="scss" scoped>

</style>
