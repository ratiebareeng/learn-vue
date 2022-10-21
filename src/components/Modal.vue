<template>
    <div class="backdrop" @click.self="closeModal">
        <div class="modal" :class="{ sale: theme === 'sale' }">
            <!-- <h1>{{ header }}</h1>
            <p>{{ subtitle }}</p> -->
            <slot>default</slot>
            <div class="actions">
                <slot name="links"></slot>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: ['header', 'subtitle', 'theme'],
    methods: {
        closeModal() {
            this.$emit('close')
        }
    }
}
</script>

<!-- scoped is expensive esp if you have many
because vue will have to load many individual styles
<style scoped>
.modal will load the selector only not all styles
-->
<style>
    .modal {
        width: 400px;
        padding: 20px;
        margin: 100px auto;
        background: wheat;
        border-radius: 10px;
    }
    .backdrop {
        top: 0;
        position: fixed;
        background: rgba(0, 0, 0, 0.5);
        width: 100%;
        height: 100%;
    }
    .modal h1 {
        color: seagreen;
        border: none;
        padding: 0;
    }
    .modal p {
        font-style: normal;
    }
    .modal .actions {
        text-align: center;
        margin: 30px 0 10px 0;
    }
    .modal .actions a {
        color: #333;
        padding: 8px;
        border: 1px solid #eee;
        border-radius: 4px;
        text-decoration: none;
        margin: 10px;
    }
    .modal.sale {
        background: burlywood;
        color: white;
    }
    .modal.sale h1 {
        color: white;
    }
    .modal.sale .actions {
        color: white;
    }
    .modal.sale a {
        color: white;
    }
</style>