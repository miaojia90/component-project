<template>
    <ul class="vue-tabs">
        <li
            v-for="item in list"
            :key="item[props.id]"
            class="tabs__item"
            :style="{
                color: item[props.id] === currentActive ? '#333' : color
            }"
            @click="handleClick(item)"
        >
            <span :ref="`tabsItem${item[props.id]}`">{{ item[props.label] }}</span>
        </li>
        <span
            class="tabs-line"
            ref="tabsLine"
            :style="{
                width: lineWidth + 'px',
                transform: 'translateX(' + translateX + 'px)',
                'background-color': activeColor
            }"
        ></span>
    </ul>
</template>
<script>
export default {
    model: {
        prop: 'currentActive',
        event: 'input'
    },
    props: {
        list: {
            type: Array,
            default: () => []
        },
        currentActive: {
            type: Number | String,
            default: ''
        },
        props: {
            type: Object,
            default: () => ({
                label: 'label',
                id: 'id'
            })
        },
        activeColor: {
            type: String,
            default: '#fee22f'
        },
        color: {
            type: String,
            default: '#ccc'
        },
        height: {
            type: String | Number,
            default: 80
        }
    },
    data () {
        return {
            lineWidth: 0,
            translateX: 0
        }
    },
    mounted () {
        this.$nextTick(() => {
            this.lineWidth = this.$refs[
                'tabsItem' + this.currentActive
            ][0].offsetWidth;
            this.translateX = this.$refs[
                'tabsItem' + this.currentActive
            ][0].offsetLeft;
        })
    },
    methods: {
        handleClick (item) {
            let current = item[this.props.id]
            this.$emit('input', current)
            this.$emit('click', item)
            this.lineWidth = this.$refs['tabsItem' + current][0].offsetWidth
            this.translateX = this.$refs['tabsItem' + current][0].offsetLeft
        }
    }
}
</script>
<style lang="scss" scoped>

ul.vue-tabs {
    position: relative;
    display: flex;
}
li.tabs__item {
    width: 30%;
    height: 50px;
    font-size: 30px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    -webkit-tap-highlight-color: transparent;
    &:last-of-type {
        margin-right: 0;
    }
}
.tabs-line {
    position: absolute;
    height: 4px;
    bottom: 0;
    left: 0;
    // transition: 0.2s transform, width;
    transition: all 0.5s;
    z-index: 10;
}
</style>
