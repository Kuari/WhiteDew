<template>
    <div>
        <el-row :gutter="20">
            <el-col :span="6" v-for="(item, index) in lists" :key="index">
                <div class="panel">
                    <el-row>
                        <el-col :span="12">
                            <div class="icon">
                                <svg-icon :icon-class="item.icon" />
                            </div>
                        </el-col>
                        <el-col :span="12">
                            <div class="info">
                                <div class="title">{{ item.title }}</div>
                                <div class="count">
                                    <countTo :startVal='0' :endVal="item.count" :duration='3000'></countTo>
                                </div>
                            </div>
                        </el-col>
                    </el-row>
                </div>
            </el-col>
        </el-row>
    </div>
</template>

<script>
import countTo from 'vue-count-to'

export default {
    components: {
        countTo
    },
    props: {
        'history': {
            type: Number,
            default: 500
        },
        'user': {
            type: Number,
            default: 39
        },
        'request': {
            type: Number,
            default: 53
        },
        "online": {
            type: Number,
            default: 6
        }
    },
    data() {
        return {
            lists: [
                {
                    'icon': 'history',
                    'title': '历史访问人数',
                    'count': this.history
                },
                {
                    'icon': 'user',
                    'title': '今日访问人数',
                    'count': this.user
                },
                {
                    'icon': 'eye',
                    'title': '今日请求次数',
                    'count': this.request
                },
                {
                    'icon': 'online',
                    'title': '当前在线人数',
                    'count': this.online
                },
            ]
        }
    },
    methods: {
    }
}
</script>

<style scoped>
.panel {
    border-radius: 10px;
    padding: 45px 20px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, .12), 0 0 6px rgba(0, 0, 0, .04);
}
.icon {
    font-size: 50px;
    text-align: center;
}
.title {
    font-size: 16px;
    color: rgba(0,0,0,0.45);
    line-height: 18px;
    margin-bottom: 12px;
    text-align: center;
}
.count {
    font-size: 20px;
    font-weight: bold;
    text-align: center;
}
</style>
