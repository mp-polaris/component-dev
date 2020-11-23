<template>
    <div>
        <FacilitatedForm class="facilitatedForm" :step="3" :inputForm="inputForm" :inputType="inputType" >
            <div slot="1">
                <el-form-item label="姓名" prop="name">
                    <el-input v-model="inputForm.name"></el-input>
                </el-form-item>
                <el-form-item label="年龄" prop="age">
                    <el-input v-model="inputForm.age"></el-input>
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
                    name: "rose",
                    age: 18,
                    gender: "男",
                    childData1: [
                        {city: '北京', address: '朝阳区'},
                        {city: '成都', address: '高新区'}
                    ],
                    childData2: [
                        {class: '高三', course: 'math'},
                            {class: '高二', course: 'english'},
                        ]
                },
                inputType: [
                    {label:'类型一',name:'type01'},
                    {label:'类型二',name:'type02'},
                    {label:'类型三',name:'type03'}
                    ],
                currentIndex: ''
            }
        },
        comments: {
            FacilitatedForm
        },
        methods: {

        },
        created() {
        }
    }
</script>

<style scoped>
    .facilitatedForm {
        margin-left: 25%;
    }
</style>
