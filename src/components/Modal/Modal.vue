<template>
    <transition class="modal-fade">
        <div class="modal-backdrop">
            <div class="modal">
                <header class="modal-header">
                    <slot name="header"> 
                        Вы действительно хотите удалить?
                    </slot>
                </header>
                <section class="modal-body">
                    <slot name="body"> 
                        Body
                    </slot>
                </section>
                <footer class="modal-footer">
                    <slot name="footer"> 
                        <button v-on:click="apply" class="btn-apply">
                            Да
                        </button>
                        <button v-on:click="close" class="btn-cancel">
                            Нет
                        </button>
                    </slot>
                </footer>        
            </div>
        </div>
    </transition>    
</template>
<script>

export default {
    name: 'modal',
    methods: {
        close() {
            this.$emit('close')
        },
        apply() {
            this.$emit('apply')
        }
    }
}
</script>

<style>
    .modal-backdrop {
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background-color: rgba(0, 0, 0, 0.3);
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .modal {
        background: #ffffff;
        display: flex;
        overflow-x:auto;
        flex-direction: column;
        box-shadow: 2px 2px 20px 1px;
    }
    .modal-header,
    .modal-footer {
        padding: 15px;
        display: flex;       
    }
    .modal-header {
        border-bottom: 1px solid #90caf9;
        color: #90caf9;
        justify-content: space-between;
    }
    .modal-footer {
        border-top: 1px solid #90caf9;
        justify-content: flex-end;
    }
    .modal-body {
        position: relative;
        padding: 20px 10px;
    }
    .modal-fade-enter,
    .modal-fade-leave-active {
        opacity: 0;
    }

    .modal-fade-enter-active,
    .modal-fade-leave-active {
        transition: opacity .5s ease
    }
    
    .btn-cancel {
       border: none;
       font-size: 20px;
       padding: 20px;
       cursor: pointer;
       font-weight: bold;
       color:cadetblue;
       background: transparent;
    }
    .btn-apply {
        color: white;
        background: #4AAE9B;
        border: 1px solid #4AAE9B;
        border-radius: 2px;
    }
</style>