<template>
    <div>
        <el-table
        stripe
        border
        :data="tableData"
        style="width: 100%; font-size: 18px"
        >
        <el-table-column label="个人信息" align="center">
            <el-table-column
                stripe
                align="center"
                label="序号"
            >
                <template slot-scope="scope">
                    <p>{{ scope.$index +1 }}</p>
                </template>
            </el-table-column>
            
            <el-table-column
                stripe
                align="center"
                prop="username"
                label="用户姓名"
                >
            </el-table-column>
                <el-table-column
                stripe
                align="center"
                prop="source"
                label="出发地"
                >
            </el-table-column>

            <el-table-column
                stripe
                align="center"
                prop="target"
                label="目的地"
                >
            </el-table-column>
        

            <el-table-column
                stripe
                align="center"
                prop="order_status"
                label="是否抢到票"
                >
                <template slot-scope="scope">
                    <div v-if="scope.row.order_status==1">
                        <p>已抢到</p>
                    </div>      
                    <div v-if="scope.row.order_status==0">
                        <p>未抢到</p>
                    </div>            
                </template>
            </el-table-column>

            <el-table-column label="操作" align="center">
                <template slot-scope="scope">
                    <el-button size="mini" type='danger' @click="delete_order(scope.row.id)">删除</el-button>
                </template>
            </el-table-column>
            
        </el-table-column>
        </el-table>
    
    </div>
    
</template>

<script>
import Card from '../components/Card'
import axios from 'axios'
import * as echarts from 'echarts'


export default {
    data() {
        return {
            tableData: '',
        }
    },
    components: {
        Card
    },
    methods: {
       getData(){
           let api = 'api/order/show_order'
           axios.get(api).then((result)=>{
           this.tableData = result.data.data
            console.log(this.tableData)
        })
       },
       delete_order(order_id){
           let api = 'api/order/delete_order'
           console.log(order_id)
           axios.post(api, `order_id=${order_id}`).then(res=>{
               console.log(res)
               this.getData()
           })

       },

    },
    mounted(){
        this.getData()
    }
}
</script>

<style>
.list-item {
    display: inline-block;
    margin-right: 10px;
}

.list-enter-active,
.list-leave-active {
    transition: all 1s;
}

.list-enter,
.list-leave-to
{
    opacity: 0;
    transform: translateY(30px);
}
.train{
    min-height: 600px;
}
.loadingBox{
    text-align: center;
    margin-top:20px;
    margin-bottom:20px;
}
.el-pagination {
    text-align: center;
    /* font-size: 20px; */
}

.comment {
    text-align: center
}

.page {
    background: white;
}



</style>
