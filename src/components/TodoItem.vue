
<script setup>
    // import Icon from '@iconify/vue'
    import { Icon } from '@iconify/vue';
    const props = defineProps({
       todo: {
            type: Object,
            required: true,
            default: () => {},
        },
        index: {
            type: Number,
            required: true,
        }
    });
    defineEmits(["toggleComplete", "edit-todo", "update-todo", "delete-todo"]);
</script>

<template>
    <div>        
        <li>
            <input type="checkbox" 
                v-bind:checked="todo.isCompleted" 
                @input="$emit('toggleComplete', index)">
            <div class="todo">
                <input 
                    v-if="todo.isEditing" type="text" 
                    v-bind:value="todo.todo" autofocus
                    @input="$emit('update-todo', $event.target.value, index)"
                /> 
                <span v-else v-bind:class="{ 'completedTodo': todo.isCompleted }">
                    {{ todo.todo }}
                </span>
            </div>
            <div class="todo-actions">
                <!-- === Check Icon === -->
                <Icon 
                    icon="ph:check-circle" class="icon"  
                    style="color: #41B080" width="22" 
                    v-if="todo.isEditing"
                    @click="$emit('edit-todo', index)"
                />
                <!-- === Pencil Icon === -->
                <Icon 
                    icon="ph:pencil-fill" class="icon"  
                    style="color: #41B080" width="22"
                    v-else 
                    @click="$emit('edit-todo', index)" 
                />
                <!-- === Trash Icon === -->
                <Icon 
                    icon="ph:trash" class="icon"  
                    style="color: #F95E5E" width="22" 
                    @click="$emit('delete-todo', todo.id)"
                />
            </div>     
        </li>
    </div>
</template>



<style lang="scss" scoped>
    li {
        display: flex;
        flex-direction: row;
        align-items: left;
        gap: 10px;
        padding: 16px 10px;
        background-color: #f1f1f1;
        box-shadow: 0 20px 25px -5px rgb(0 0 0 / 0.1),
            0 8px 10px -6px rgb(0 0 0 / 0.1);
        width: 80%;
        margin: 0 auto;
        &:hover{
            .todo-actions {
                opacity: 1;
            }
        }

        input[type=checkbox] {
            appearance: none;
            width: 20px;
            height: 20px;
            background-color: #fff;
            border-radius: 50%;
            box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);
            &:checked {
                background-color: #41b080;
            }
        }

        .todo {
            flex: 1;

            .completedTodo {
                text-decoration: line-through;
            }
            input[type=text] {
                width: 100%;
                padding: 2px 6px;
                border: 2px solid #41B080;
                font-size: 16px;
                font-weight: 400;
            }
        }

        .todo-actions {
            display: flex;
            gap: 6px;
            opacity: 0;
            transition: 150ms ease-in-out;
            .icon {
                cursor: pointer;
            }
        }
    }
</style>