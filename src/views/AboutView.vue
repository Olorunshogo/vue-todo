
<script>
    export default {
        data() {
            return {
                header: 'Vue Todos'
            }
        },
    }
</script>

<template>
    <div>
        <h1>{{ header }}</h1>
        <p>Vue Todos is a <span class="bold">CRUD</span> (Create, Read, Update and Delete) Todo tracking application.</p>
        <p>Track your daily tasks using this todo tracker with abilities to save, complete, edit and delete todos.</p>
        <p>Feel free to add on to this application with functionalities such as the ability to drag and reorder todos, animate creation and deletion of todos or even create this into a full stack application with the ability to have different lists for different days of tracking todos!</p>
    </div>
</template>

<style scoped>
    p {
        font-size: 16px;
        margin: 0 0 12px 12px;
    }

    .bold {
        font-weight: bold;
    }
</style>