<template>
    <div class="contain">
        <leftBox class="dataBox" />
        <contentBox class="dataBox" />
        <rightBox class="dataBox" />
    </div>
</template>
<script>

import leftBox from '@/views/components/leftBox'
import contentBox from '@/views/components/contentBox'
import rightBox from '@/views/components/rightBox'
export default {
    name: '',
    components: {
        leftBox,
        contentBox,
        rightBox
    },
    props: {

    },
    data() {
        return {

        }
    },
    computed: {

    },
    watch: {

    },
    mounted() {

    },
    methods: {

    }
};
</script>
<style lang='scss' scoped>
.contain {
    display: flex;
    box-sizing: border-box;
    flex-direction: row;
    width: 100vw;
    height: 100vh;
    background-color: rgba(1, 19, 47, 0.9);
    padding: 2vh;

    .dataBox {
        box-sizing: border-box;
        box-shadow: 0 0 8px 1px rgb(136, 0, 255),
            0 0 8px 1px rgb(136, 0, 255) inset;

        padding: 1vh;
    }

    .dataBox:nth-child(2) {
        margin: 0 2vh;
    }

    .leftBox {
        flex: 1;
    }

    .contentBox {
        flex: 2;
    }

    .rightBox {
        flex: 1;
    }
}
</style>