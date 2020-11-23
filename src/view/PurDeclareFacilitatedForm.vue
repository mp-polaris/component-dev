<template>
    <div>
        <FacilitatedForm class="facilitatedForm" :step="3" :inputForm="inputForm" :inputType="inputType" @currentTypeIndex="setCurrentTypeIndex">
            <div slot="step01">
                <el-form-item label="姓名" prop="username">
                    <el-input v-model="inputForm.username"></el-input>
                </el-form-item>
                <el-form-item label="年龄" prop="age" v-show="currentTypeIndex == 1">
                    <el-input v-model="inputForm.age"></el-input>
                </el-form-item>
                <el-form-item label="性别" prop="gender" v-show="currentTypeIndex == 2">
                    <el-input v-model="inputForm.gender"></el-input>
                </el-form-item>
            </div>
            <div slot="step02">
                <el-table :data="inputForm.childData1" style="width: 40%; margin: 30px auto;">
                    <el-table-column prop="city" label="城市" width="180"></el-table-column>
                    <el-table-column prop="address" label="地址" width="180"></el-table-column>
                </el-table>
                <el-button type="primary"
                           style="margin-left: 65%"
                           @click="[dialogFormVisible = true,inputForm.childData1.push( {city: '', address: ''})]">增加</el-button>

                <el-dialog title="step02" :visible="dialogFormVisible">
                    <el-form-item label="城市" prop="city">
                        <el-input v-model="inputForm.childData1[inputForm.childData1.length - 1].city"></el-input>
                    </el-form-item>
                    <el-form-item label="地址" prop="address">
                        <el-input v-model="inputForm.childData1[inputForm.childData1.length - 1].address"></el-input>
                    </el-form-item>
                    <el-button type="primary" @click="dialogFormVisible = false">确定</el-button>
                </el-dialog>
            </div>
            <div slot="step03">
                <el-form-item label="年级" prop="class">
                    <el-input v-model="inputForm.childData2[1].class"></el-input>
                </el-form-item>
                <el-form-item label="课程" prop="course">
                    <el-input v-model="inputForm.childData2[1].course"></el-input>
                </el-form-item>
            </div>
        </FacilitatedForm>

    </div>
</template>

<script>
    import FacilitatedForm from '@/components/FacilitatedForm'

    export default {
        components: {FacilitatedForm},
        data() {
            return {
                inputForm: {
                    username: "rose",
                    age: 18,
                    gender: "男",
                    childData1: [
                        {city: '北京', address: '朝阳区'},
                        {city: '成都', address: '高新区'}
                    ],
                    childData2: [
                        {class: '高二', course: 'english'},
                        {class: '高三', course: 'math'}
                    ]
                },
                inputType: [
                    {label:'类型一',name:'type01'},
                    {label:'类型二',name:'type02'},
                    {label:'类型三',name:'type03'}
                    ],
                currentTypeIndex: '',
                dialogFormVisible: false
            }
        },
        methods: {
            setCurrentTypeIndex(currentTypeIndex){
                this.currentTypeIndex = currentTypeIndex
            }
        },
        mounted() {
            console.log(this.currentTypeIndex)
        }
    }
</script>

<style scoped>
    .facilitatedForm {
        margin-left: 20%;
    }
     .el-table::before {
         width: 0;
     }
</style>
