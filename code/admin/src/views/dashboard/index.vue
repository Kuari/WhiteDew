<template>
    <div class="container">
        <div class="line1">
            <panelGroup></panelGroup>
        </div>
        <div class="line2">
            <el-row :gutter="20">
                <el-col :span="12">
                    <div class="panel">
                        <pieChart></pieChart>
                    </div>
                </el-col>
                <el-col :span="12">
                    <div class="panel">
                        <!--<barchart></barchart>-->
                    </div>
                </el-col>
            </el-row>
        </div>
    </div>
</template>

<script>
import panelGroup from './components/panelGruop.vue'
import pieChart from './components/PieChart.vue'

export default {
    name: 'Dashboard',
    components: {
        panelGroup,
        pieChart
    }
}
</script>

<style scoped>
.panel {
    border-radius: 10px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, .12), 0 0 6px rgba(0, 0, 0, .04);
    padding: 20px;
    height: 400px;
}
.line1 {
    margin-bottom: 20px;
}
</style>
