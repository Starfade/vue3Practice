<template>
    <div>
        <el-button type="danger" @click="open">点我点我快点我</el-button>
        <br>
        <el-button v-if="status" type="warning" @click="open2">达咩达咩达咩哟</el-button>
        <el-table :data="tableData" border style="width: 100%">
            <el-table-column prop="date" label="Date" width="180" />
            <el-table-column prop="name" label="Name" width="180" />
            <el-table-column prop="status" label="Status" width="180" />
            <el-table-column prop="address" label="Address" />
        </el-table>
    </div>
</template>
<script lang="ts" setup>
import { ref } from 'vue'
let bool: boolean = true
const status = ref(bool)
let num = 0
let tableData = ref([
    {
        date: '2016-05-03',
        name: 'Tom',
        address: 'No. 189, Grove St, Los Angeles',
        status: status
    },
    {
        date: '2016-05-02',
        name: 'Tom',
        address: 'No. 189, Grove St, Los Angeles',
        status: status
    },
    {
        date: '2016-05-04',
        name: 'Tom',
        address: 'No. 189, Grove St, Los Angeles',
        status: status
    },
    {
        date: '2016-05-01',
        name: 'Tom',
        address: 'No. 189, Grove St, Los Angeles',
        status: status
    },
])
function open() {
    // ElMessage({
    //     message: '哟，你点击了我',
    //     type: 'success'
    // })
    ElNotification({
        type: 'success',
        message: '哟，你点击了我',
        duration: 3000,
    })
    if (status.value == false) {
        setTimeout(() => {
            num = 0
            status.value = true
            ElNotification({
                type: 'info',
                message: '不知怎么的，按钮2看到你点击了按钮1后又跑回来了',
                duration: 3000,
            })
        }, 500);
    }
}
let open2 = () => {
    ElMessageBox.alert('呀！hentai！', '达咩跌死', {
        confirmButtonText: '再点！',
        callback: (action: any) => {
            num++
            if (action == 'confirm' || num >= 3) {
                status.value = !status.value
                // ElMessage({
                //     message: '你过于变态的行为把按钮2吓跑了',
                //     type: 'error'
                // })
                ElNotification({
                    type: 'error',
                    message: '你过于变态的行为把按钮2吓跑了',
                    duration: 3000,
                })
            }
        }
    })
}
</script>
<style lang="less"></style>