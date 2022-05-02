<template>
    <div class="dialogue" v-if="show" @click.self="hideModal">
        <div class="dialogue__content">
            <slot></slot>
        </div>
    </div>
</template>

<script>
export default {
    name: "my-dialogue",

    props: {
        show: {
            type: Boolean,
            default: false
        }
    },

    methods: {
        hideModal() {
            this.$emit('update:show', false)
        }
    }
}
</script>

<style>
.dialogue {
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
    background: rgba(0, 0, 0, 0.5);
    position: fixed;
    display: flex;
}

.dialogue__content {
    margin: auto;
    background: white;
    border-radius: 12px;
    min-height: 50px;
    min-width: 300px;
}
</style>