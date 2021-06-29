<template>
    <div class="bg" v-if="isShow">
        <div class="modal-container">
            <h2 class="modal-title">{{title}}</h2>
            <slot />
        </div>
    </div>
</template>

<script>
export default {
    name: 'Modal',
    props: {
        title: {
            type: String
        },
        isShow: {
            type: Boolean
        }
    }
}
</script>

<style scoped>
    .bg {
        position: fixed;
        left: 0;
        right: 0;
        top: 0;
        bottom: 0;
        background: rgba(0, 0, 0, 0.6);
    }
    .modal-container {
        position: absolute;
        top: 30%;
        left: 50%;
        transform: translate(-50%, -30%);
        display: inline-block;
        max-width: 500px;
        width: 95%;
        background: #fff;
        border-radius: 5px;
    }
</style>