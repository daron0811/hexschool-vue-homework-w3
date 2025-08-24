<template>
    <tr v-for="item in cart" :key="item.id">
        <td><!--操作-->
            <button type="button" class="btn btn-sm" @click="removeFromCart(item.id)">
                x
            </button>
        </td>
        <td>{{ item.name }}</td><!--品項-->
        <td><small>{{ item.description }}</small></td><!--描述-->
        <td><!--數量-->
            <select class="form-select" v-model="item.quantity" @change="updateCart(item)">
                <option v-for="n in 10" :key="n" :value="n">{{ n }}</option>
            </select>
        </td>
        <td>{{ item.price }}</td><!--單價-->
        <td>{{ itemSubtotal(item) }}</td><!--這品項總計-->
    </tr>
</template>

<script setup>

const props = defineProps({
    cart: { type: Object, require: true }
})

const emit = defineEmits(['update', 'delete'])

const itemSubtotal = (item) => {
  return item.price * item.quantity;
};

const removeFromCart = (id) => {
    emit('delete',id);
};

const updateCart = (item) => {
  emit('update',item);
};
</script>