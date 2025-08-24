<template>
    <div class="toast-container position-fixed top-0 end-0 p-3">
        <div ref="toastEl" class="toast" role="alert" aria-live="assertive" aria-atomic="true">
            <div class="toast-header">
                <strong class="me-auto">{{ title }}</strong>
                <small>{{ time }}</small>
                <button type="button" class="btn-close" data-bs-dismiss="toast" aria-label="Close"></button>
            </div>
            <div class="toast-body">
                {{ message }}
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, watch, onMounted } from 'vue'
import * as bootstrap from 'bootstrap'

// 定義 props
const props = defineProps({
    title: { type: String, default: '系統通知' },
    message: { type: String, required: true },
    time: { type: String, default: '剛剛' },
    show: { type: Boolean, default: false }
})

const toastEl = ref(null)
let toastInstance = null

onMounted(() => {
    toastInstance = new bootstrap.Toast(toastEl.value, {
        delay: 3000,
        autohide: true
    })
})

// 監聽 show 狀態 → true 時顯示 Toast
watch(
    () => props.show,
    (newVal) => {
        if (newVal) {
            toastInstance.show()
        }
    }
)
</script>
