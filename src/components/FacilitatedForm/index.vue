<template>
    <div class="mw1000 center-block">
        <div class="panel">
            <div class="panel-body text-center">
                <div class="row wizard-options">

                    <div class="ph10"
                         :class="['col-sm-' + 12/inputType.length,'col-xs-' + 12/inputType.length]"
                         v-for="(type,index) in inputType" :key="type.name"
                         @click="exchangeType(index)">
                        <a class="holder-style p15" :class="{'holder-active':currentTypeIndex == index}">
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
                <el-step :title="'步骤' + num" v-for="num in step" :key="num"></el-step>
            </el-steps>

            <el-form
                    label-position="right"
                    label-width="80px"
                    :model="inputForm">
                <div v-show="active == index" v-for="(num,index) in step" :key="num">
                    <slot :name="'step0' + num"></slot>
                </div>
            </el-form>

            <el-button style="float:right;margin-top:50px;margin-right:28%;" :disabled="active!=step" @click="save">保存
            </el-button>
            <el-button style="float:right;margin-top:50px;margin-right:2%;" :disabled="active==step" @click="next">下一步
            </el-button>
            <el-button style="float:right;margin-top:50px;margin-right:2%;" :disabled="active==0" @click="last">上一步
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
                currentTypeIndex: 0,//当前分类下标
                active: 0,//步骤条
            };
        },
        methods: {
            exchangeType(index) {
                this.currentTypeIndex = index
                this.$emit('currentTypeIndex', this.currentTypeIndex)
                this.active = 0;
                //对主表和附表数据进行置空处理
                Object.keys(this.inputForm).forEach(key => {
                    if(!(this.inputForm[key] instanceof Array)) {
                        this.inputForm[key] = ''
                    } else {
                        this.inputForm[key].forEach(function(e){
                            Object.keys(e).forEach(key => {
                                e[key] = ''
                            })
                        });
                    }
                })
            },
            last() {
                if (this.active-- < 0) this.active = 0;
            },
            next() {
                if (this.active++ > this.step) this.active = this.step;
            },
            save() {
                console.log(this.inputForm)
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
