
<script setup>
    import { reactive } from "vue"; 
    import TodoButton from './TodoButon.vue'
    const emit = defineEmits(["create-todo"]);

    const todoState  = reactive({
        todo: "",
        invalid: null,
        errorMsg: "",
    });

    // Each time the createTodo() is called
    const createTodo = () => {
        // Resetting the invalid property of the input field when empty to null.
        todoState.invalid = null;
        // Check so as not to return empty.
        if(todoState.todo !== "") {
            emit("create-todo", todoState.todo);
            todoState.todo = "";
            return;
        }
        // Let the user sha know that the input field is empty.
        todoState.invalid = true;
        todoState.errorMsg = "Todo value cannot be empty!!!";
    }
</script>

<template>
    <div class="input-wrapper" v-bind:class="{ 'input-err': todoState.invalid }">
        <input type="text" name="text" v-model="todoState.todo" autofocus>
        <TodoButton v-on:click="createTodo($event)"></TodoButton>
    </div>
    <!-- Create and destroy each time it is invalid and valid respectively -->
    <!-- <p v-if="todoState.invalid" class="error-msg">{{ todoState.errorMsg }}</p> -->
    <!-- Only create initially and subsequently add the display none CSS property when invalid or not. -->
    <p v-show="todoState.invalid" class="error-msg">{{ todoState.errorMsg }}</p>
</template>

<style lang="scss" scoped>
    .input-wrapper {
        display: flex;
        flex-direction: row;
        transition: 250ms ease;
        border: 2px solid #41b080;
        width: 90%;
        margin: 0 auto;

        &.input-err {
            border: 1px solid red;
        }

        &focus-within {
            box-shadow: 0 -4px 6px -1px rgb(0 0 0 / 0.1),
                0 -2px 4px -2px rgb(0 0 0 / 0.1);
        }

        input {
            width: 100%;
            padding: 8px 6px;
            border: none;
            &:focus {
                outline: none;
            }
        }
    }

    .error-msg {
        margin-top: 6px;
        font-size: 12px;
        text-align: center;
        color: red;
    }

</style>