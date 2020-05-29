<!--
 * @Title: 
 * @Package: 
 * @Descripttion: 
 * @Author: Major.Miao
 * @Date: 2020-05-28 17:54:44
 * @Version: V1.0
 * @Copyright: Shenzhen Hive Box Technology Co.,Ltd All rights reserved.
 * @Note: This content is limited to the internal circulation of Hive Box, and it is prohibited to leak or used for other commercial purposes.
-->
<template>
    <div>
        <!-- 默认配置 -->
        <Tabs v-model="active" :list="list" @click="handleClick" />
        <div
            class="active-box"
            :style="{
                transform: `translate(${active == 1 ? '0' : '-100%'},0)`
            }"
        >
            active-box-1
        </div>
        <div
            class="active-box"
            :style="{
                transform: `translate(${active == 2 ? '0' : '-100%'},0)`
            }"
        >
            active-box-2
        </div>
        <div
            class="active-box"
            :style="{
                transform: `translate(${active == 3 ? '0' : '-100%'},0)`
            }"
        >
            active-box-3
        </div>
        <!-- 使用自定义配置 -->
        <Tabs
            v-model="activeName"
            :list="tabList"
            @click="handleClick"
            :props="props"
        />
    </div>
</template>

<script>
import Tabs from '@/components/vue-tabs'
export default {
    name: 'register',
    components: { Tabs },
    data () {
        return {
            // 默认配置
            active: 1,
            list: [
                { id: 1, label: '项目一' },
                { id: 2, label: '我是超长项目' },
                { id: 3, label: '项目三' }
            ],

            // 自定义配置
            activeName: 1,
            tabList: [
                { number: 1, text: 'tabs1' },
                { number: 2, text: 'tabs2' }
            ],
            props: {
                label: 'text',
                id: 'number'
            }
        }
    },
    methods: {
        handleClick (item) {
            console.log(item)
        }
    }
}
</script>
<style lang="scss" scoped>
.active-box {
    width: 100%;
    background-color: #fff;
    height: 300px;
    font-size: 30px;
    position: relative;
    transition: all 0.9s ease;
}
</style>
