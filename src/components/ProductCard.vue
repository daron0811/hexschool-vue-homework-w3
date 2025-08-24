<template>
    <a v-for="drink in drinks" :key="drink.id" href="#" class="list-group-item list-group-item-action"
        @click.prevent="addToCart(drink)">
        <div class="d-flex w-100 justify-content-between">
            <h5 class="mb-1">{{ drink.name }}</h5>
            <small>${{ drink.price }}</small>
        </div>
        <p class="mb-1">{{ drink.description }}</p>
    </a>
    <!-- <h3>{{props.title}}</h3> -->
</template>

<script setup>
import { ref } from 'vue';

//傳入的商品
const props = defineProps({
    drinks: { type: Object, require: true } //原本變數就是drinks，偷懶就直接傳入Object不改了XD
})

const emit = defineEmits(['cart-item'])

const addToCart = (drink) => {
    emit('cart-item', drink) // 傳出飲料物件給App
    console.log(`準備從子物件傳出的 ID : ${drink.id}`);
}

</script>