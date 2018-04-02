<template>
    <div>
        <div class="m-b-20 ovf-hd">
            <div class="fl w-200 m-l-30">
                <el-input placeholder="请输入用户名" v-model="realname">
                    <el-button slot="append" icon="search" @click="search()"></el-button>
                </el-input>
            </div>
        </div>
        <el-table
                :data="tableData"
                style="width: 100%"
                @selection-change="selectItem">
            <el-table-column
                    type="selection"
                    width="50">
            </el-table-column>
            <el-table-column
                    prop="title"
                    label="标题"
                    width="300">
            </el-table-column>
            <!--<el-table-column-->
                    <!--label="操作"-->
                    <!--width="200">-->
                <!--<template scope="scope">-->
                    <!--<div>-->
            <!--<span>-->
              <!--<router-link :to="{ name: 'usersEdit', params: { id: scope.row.id }}" class="btn-link edit-btn">-->
            <!--编辑-->
              <!--</router-link>-->
            <!--</span>-->
                        <!--<span>-->
              <!--<el-button size="small" type="danger" @click="confirmDelete(scope.row)">删除</el-button>-->
            <!--</span>-->
                    <!--</div>-->
                <!--</template>-->
            <!--</el-table-column>-->
        </el-table>
        <div class="pos-rel p-t-20">
            <btnGroup :selectedData="multipleSelection" :type="'users'"></btnGroup>
            <div class="block pages">
                <el-pagination
                        @current-change="handleCurrentChange"
                        layout="prev, pager, next"
                        :page-size="limit"
                        :current-page="currentPage"
                        :total="dataCount">
                </el-pagination>
            </div>
        </div>
    </div>
</template>

<script>
  import http from '../../../assets/js/http'

  export default {
    data() {
      return {
        tableData: [],
        multipleSelection: []
      }
    },
    methods: {
      selectItem(val) {
        this.multipleSelection = val
      }
    },
    created() {
      this.apiGet('report/auctioningitems').then((res) => {
        this.handelResponse(res, (data) => {
          this.tableData = data
        })
      })
    },
    computed() {
    },
    components: {},
    mixins: [http]
  }
</script>

