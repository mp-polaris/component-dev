<template>
    <div class="mw1000 center-block">
        <div class="panel">
            <div class="panel-body text-center">
                <div class="row wizard-options">

                    <div class="ph10"
                         :class="['col-sm-' + 12/inputType.length,'col-xs-' + 12/inputType.length]"
                         v-for="(type,index) in inputType" :key="type.name"
                         @click="exchangeType(index)">
                        <a class="holder-style p15" :class="{'holder-active':currentIndex == index}">
                            <span class="fa fa-align-left holder-icon"></span>
                            <br/>
                            {{type.label}}
                        </a>
                    </div>

                </div>
            </div>
        </div>

        <div class="admin-form">
            <el-steps
                    :active="active"
                    finish-status="success"
                    simple
                    style="margin-top: 20px"
            >
                <el-step title="步骤 1"></el-step>
                <el-step title="步骤 2"></el-step>
                <el-step title="步骤 3"></el-step>
            </el-steps>

            <el-form
                    label-position="right"
                    label-width="80px"
                    :model="inputForm">
                <div>
                    <solt name="1"></solt>
                </div>
                <solt name="2"></solt>
                <solt name="3"></solt>

            </el-form>

            <el-button style="float:right;margin-top:50px;margin-right:28%;" :disabled="active!=3" @click="save">保存
            </el-button>
            <el-button style="float:right;margin-top:50px;margin-right:2%;" :disabled="active==3" @click="next">下一步
            </el-button>
            <el-button style="float:right;margin-top:50px;margin-right:2%;" :disabled="active==1" @click="last">上一步
            </el-button>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            inputForm: {
                type: Object,
                default: function () { return {} }
            },
            inputType: {
                type: Array,
                default: function () { return [] }
            },
            step: Number
        },
        data() {
            return {
                currentIndex: 0,//当前分类下标
                active: 1,//步骤条
            };
        },
        computed: {
            // newTypes(){
            //     let _this = this
            //      return this.inputType.filter(function (item,index) {
            //         if(_this.currentIndex == index && _this.active == 1) return true;
            //     });
            // }
        },
        methods: {
            exchangeType(index) {
                this.currentIndex = index
                this.$emit('currentIndex', this.currentIndex)
                this.active = 1;
                Object.keys(this.inputForm).forEach(key => {
                    this.inputForm[key] = ''
                })
            },
            last() {
                if (this.active-- < 1) this.active = 1;
            },
            next() {
                if (this.active++ > 2) this.active = 2;
            },
            save() {

            },
        }
    };
</script>

<style>
    @import "../../assets/skin/default_skin/css/theme.css";
    @import "../../assets/admin-tools/admin-forms/css/admin-forms.css";

    .el-steps--simple {
        margin: 15px 50px;
    }

    .admin-form {
        background: #ffffff;
        height: 500px;
        overflow: hidden;
    }

    .admin-form .el-form-item {
        margin: 0;
        margin-left: 20%;
    }

    .admin-form .el-input__inner {
        width: 60%;
        height: 30px;
    }
</style>
