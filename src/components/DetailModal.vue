<template>
    <div class="black-bg" v-if="detailIsOpened">
        <div class="white-bg">
            <img :src="products[viewIdx].image" alt="" width="100%">
            <h4>{{ products[viewIdx].title }}</h4>
            <p>{{ products[viewIdx].content }}</p>
            <!--<input @input="month = $event.target.value">-->
            <input v-model="month">
            <p> {{ month }}개월 선택함 : {{ month * products[viewIdx].price }} 원</p>
            <button @click="closeDetail">닫기</button>
        </div>
    </div>
</template>

<script>
export default {
    name: "DetailModal",
    data() {
        return {
            month: 1
        }
    },
    watch: {
        month(v, before) {
            this.month = v.trim();
            if(isNaN(v)) {
                alert('숫자만 입력 가능합니다.')
                this.month = before;
            } else if(v >= 13 || v <= 0) {
                alert('1~12사이의 숫자만 입력 가능합니다.')
                this.month = before;
            }
        }
    },
    props: {
        products: Array,
        detailIsOpened: Boolean,
        viewIdx: Number
    },
    methods: {
        closeDetail() {
            this.$emit('closeDetail');
            this.month = 1;
        }
    }
}
</script>

<style scoped>
.black-bg {
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
    position: fixed;
    padding: 20px;
}

.white-bg {
    width: 100%;
    background: white;
    border-radius: 8px;
    padding: 20px;
}
</style>