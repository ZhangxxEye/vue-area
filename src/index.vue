<template>
    <div class="area"v-show="isShow">
        <div class="popcover"></div>
        <div class="con">
            <div class="head">
                <span class="title">所在地区</span>
                <span class="close" @click="closeFn"></span>
            </div>
            <div class="selected">
                <span class="sel pro" :class="{active:active_index==1}" @click="sel_pro">{{pro.name}}</span>
                <span class="sel city" :class="{active:active_index==2}" @click="sel_city">{{city.name}}</span>
                <span class="sel dis" :class="{active:active_index==3}" @click="sel_dis" v-show="is_show_dis">{{dis.name}}</span>
            </div>
            <div class="list_wrap">
                <div class="list">
                    <ul v-show="active_index==1">
                        <li class="list_item" v-for="(item,index) in pro.data" :key="index" @click="pro_click(item)">
                            {{item.name}} <em :class="{active:pro.id==item.id}"></em></li>
                    </ul>
                    <ul v-show="active_index==2">
                        <li class="list_item" v-for="(item,index) in city.data" :key="index" @click="city_click(item)">
                            {{item.name}} <em :class="{active:city.id==item.id}"></em></li>
                    </ul>
                    <ul v-show="active_index==3">
                        <li class="list_item" v-for="(item,index) in dis.data" :key="index" @click="dis_click(item)">
                            {{item.name}} <em :class="{active:dis.id==item.id}"></em></li>
                    </ul>
                </div>
            </div>
        </div>
    </div>
</template>
<style lang="less">
    * {
        -webkit-tap-highlight-color: transparent;
    }

    .area {
        width: 100%;
        height: 100%;
        position: absolute;
        top: 0;
        left: 0;
        z-index: 3;

        .popcover {
            position: fixed;
            top: 0;
            bottom: 0;
            left: 0;
            right: 0;
            background-color: #000;
            opacity: 0.8;
        }

        .con {
            position: fixed;
            bottom: 0;
            display: flex;
            flex-direction: column;
            width: 100%;
            top: 164px;
            background: rgba(255, 255, 255, 1);
            border-radius: 30px 30px 0px 0px;

            .head {
                width: 100%;
                padding: 25px;
                height: 26px;
                text-align: center;
                position: relative;
                display: flex;
                align-items: center;
                justify-content: center;
                box-sizing: border-box;

                .title {
                    font-size: 16px;
                }

                .close {
                    position: absolute;
                    right: 20px;
                    display: inline-block;
                    width: 13px;
                    height: 13px;
                    background: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABoAAAAaCAYAAACpSkzOAAABlElEQVRIS63WsUoDQRAG4H9SWIUI6S97vkIstBIUwTa9diJY6gPYpBaxExEfQVGwsLLxFcQHmLWxuUK4JsWO7JE7zmTvdjfnlpfNfNnszM8RACRJMgGwobW+BiD2WdellBobYyZ5nl9mWfZDFiGiBwA9EbnXWp90xdI03TbGvAJYB/DOzDsWOieiq/IEXbEFxJb9YmZFACx2R0THXTEH8g1gj5k/LWRXZ6wNKYDapa+M+ZBFaKWThSAuKAoLRZqgICwGaYNasTRNt2pzYvdW3dU06PVmcO1ZahAiehKR3fkwBiG+E5XwElb7Rd6TVEUCM42UUo8iYjOxXDMR2dRaf4TU8P11RQ3HxRfPY+LKCzmQGYC18hShWCvkamER2QdwFpuNjZBnTqLjygkFDmMUtgQFIo2t33Rnf6BIJAqroBWRYKyAOiJBmJ34sYi8xWZXQxq44uqWmU/tB1Miuph/MTi7WmJnEcuZeUDD4XDQ7/df7HsdgAP7IhGSXZ49NBqNbgAcicih1vq53nU9AOYfkHqJquYvOkOJLizy6k8AAAAASUVORK5CYII=") no-repeat;
                    background-size: 13px 13px;
                }
            }

            .selected {
                width: 100%;
                height: 62px;
                padding: 26px 25px 0 25px;
                background-color: #fafafa;
                box-sizing: border-box;
                overflow: hidden;
                white-space: nowrap;
                text-overflow: ellipsis;

                .sel {
                    font-size: 16px;
                    margin-right: 25px;
                }

                .sel.active {
                    padding-bottom: 5px;
                    border-bottom: 1px solid #ffc800;
                    border-bottom-left-radius: 1px;
                    border-top-right-radius: 1px;
                }
            }

            .list_wrap {
                flex: 1;
                overflow-y: auto;

                .list {
                    margin: 25px;
                }

                .list_item {
                    font-size: 16px;
                    line-height: 16px;
                    margin-bottom: 25px;

                    .active {
                        display: inline-block;
                        width: 17px;
                        height: 17px;
                        background: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACIAAAAiCAYAAAA6RwvCAAACaUlEQVRYR+2VP2hTcRDHP/eSSq0ianUS/DNUF8c0fxqHIgixqNilRBClm1oXJxcR/yxOTmqpg+jSoUqh6iKiqVrT/BFUHJyUUhF0KaiDlJp3kkcS3ntJ+pIUnx3y1rvf3ee+d/dOWCWfrBIO2iDuTrQV+a+KaJrNCDv5wnsZomCH8a01mucABR4AG4AZguyXEEtlGF9ANE0Yg2fA+ooKJv3SxwvfQDTPHgrMAFtsrVhC2S0x5nwB0TTbMHgN7HAN51mJctOXGdFXbGINL1H2uiCuSpSLvmyNplmLwVMg7kgojEmEU7XOStWw6gQBtjOIgckcU+4187pNmiJIF5Moh12+k8wzVC9eNUiWuygnS0GmCXJUQvzwAijbNcMdYNjlP003CelhsV6capBZfiG2NYMPmByUPr56wWiWayjnXe14R4B+r2JqKfII5ZAjmDIPJCTGx3owmuUcynWX/TMGcQnzzauIapDitHfwENjnerxAgCPSa62jkzPDcYR7KIbN8J0gcQnxyQuiaK/5Z9UUnXQxjjLoCvIbOCZRpiozkSOBaYF32Hx/Wu3o5W0jEHVBigYtVpfjBsppV5sKGIxIhDF9Q4Q/1q97XcVHWcRgQCI8bxRiWZBKxbNcQLjiUE9QlFtAEui2JSxe1KRErePW1NfQ0dMcw5jcBoJ1oxfhTEYkxmhTBCXnhkCsVmUYACYcbbBnVC5LjEutQDTUGkeuPGFMHqNsdSQURiXCmVYhmgYpKdMDPAF2WYmF+4RJimD6CmLBpNhIJycQFogwvlKIlhRZSdXLvW14WP8VQDluG8StcFuRtiJeW/cXeOmfI+FjOH4AAAAASUVORK5CYII=") no-repeat;
                        background-size: 17px 17px;
                        vertical-align: middle;
                    }
                }

                .active {
                    color: #ffc800;
                }
            }
        }
    }
</style>
<script>
    import '../src/common/css/reset.css';
    export default {
        props: {
            areaList: {
                type: Array
            },
            areaIds: {
                default: "",
                type: String
            }
        },
        data() {
            return {
                isShow: true,
                area_data: [],
                cur_data: [],
                active_index: 1,
                txt: "请选择",
                pro: {
                    data: [],
                    id: "",
                    show: true,
                    name: "请选择"
                },
                city: {
                    data: [],
                    id: "",
                    show: true,
                    name: "请选择"
                },
                dis: {
                    data: [],
                    id: "",
                    show: true,
                    name: "请选择"
                },
                lastTop: 0,
                is_show_dis: true,
                initState: false
            };
        },
        watch: {
            areaIds(val) {
                // 初始化未完成的情况下，接收到父组件传值后，调用初始化方法。
                if (this.initState == false) {
                    this.initData();
                }
            },
            areaList (val) {
                this.area_data = this.areaList;
                this.pro.data = this.areaList;
            }
        },
        methods: {
            initData() {
                // 若此刻父组件未将areaIds传递过来，不进行初始化。待watch监控到areaIds有值时，会主动调用初始化，标记为初始化已完成。
                if (this.areaIds) {
                    console.log('-----------');
                    let ids = this.areaIds.split(",");
                    let _pro = this.pro.data.filter(item => item.id == ids[0]);
                    if (_pro.length) {
                        this.pro.id = ids[0];
                        this.pro.name = _pro[0].name;
                        let index_id = 0;
                        if (ids[0] == ids[1] && ids.length == 3) {
                            // 只有省级城市
                            index_id = 2;
                        } else {
                            index_id = 1;
                        }
                        let _city = _pro[0].subcat.filter(item => item.id == ids[index_id]);
                        if (_city.length) {
                            this.city.id = index_id == 1 ? _city[0].id : ids[2];
                            this.city.name = _city[0].name;
                            this.city.data = _pro[0].subcat;
                            if (index_id == 1) {
                                let _dis = _city[0].subcat.filter(item => item.id == ids[2]);
                                if (_dis.length) {
                                    this.dis.id = ids[2];
                                    this.dis.name = _dis[0].name;
                                    this.dis.data = _city[0].subcat;
                                }
                            }
                            this.$emit("areaDone", {
                                pro: this.pro,
                                city: index_id == 1 ? this.city : {},
                                dis: index_id == 1 ? this.dis : this.city
                            });
                        }
                    }
                    this.initState = true; // 初始化完成
                }
            },
            sel_pro() {
                this.active_index = 1;
            },
            sel_city() {
                this.active_index = 2;
            },
            sel_dis() {
                this.active_index = 3;
            },
            pro_click(obj) {
                let _data = this.pro.data.filter(item => item.id == obj.id);
                this.pro.id = obj.id;
                this.city.name = this.txt;
                this.dis.name = this.txt;
                this.city.id = "";
                this.dis.id = "";
                this.dis.data = [];
                if (_data.length) {
                    this.active_index = 2;
                    this.city.data = _data[0].subcat;
                    this.pro.name = obj.name;
                }
            },
            city_click(obj) {
                let _data = this.city.data.filter(item => item.id == obj.id);
                this.city.id = obj.id;
                this.dis.name = this.txt;
                this.dis.id = "";
                this.dis.data = [];
                if (_data.length) {
                    this.dis.data = _data[0].subcat;
                    this.city.name = obj.name;
                    if (this.dis.data) {
                        this.is_show_dis = true;
                        this.active_index = 3;
                    } else {
                        this.is_show_dis = false;
                        this.$emit("areaDone", {pro: this.pro, city: {}, dis: this.city});
                    }
                }
            },
            dis_click(obj) {
                this.dis.id = obj.id;
                this.dis.name = obj.name;
                this.active_index = 3;
                this.$emit("selected", {pro: this.pro, city: this.city, dis: this.dis});
                this.isShow = false;
            },
            closeFn() {
                this.isShow = false;
            }
        },
        created() {
            this.$nextTick(() => {
                this.initData();
            });
        }
    };
</script>

