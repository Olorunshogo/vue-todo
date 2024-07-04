
<script setup>
    const props = defineProps({
       todo: {
            type: Object,
            required: true,
        },
    });
</script>

<template>
    <div>
        
        <li>
            <input type="checkbox">
            <div class="todo">
                <input type="text">
                <span>
                    {{ todo.todo }}
                </span>
            </div>
        </li>
    </div>
</template>



<style lang="scss" scoped>

</style>