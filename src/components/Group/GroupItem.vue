<template>
    <li class="group-item">
        {{item.title}}
    </li>
</template>

<script>
export default {
    props: ['item']
}
</script>

<style>
    .group-item {
        width: 100%;
        height: 30px;
        background: #f9fbe7;
        list-style: none;
        margin: 0.1rem 0;        
    }
</style>