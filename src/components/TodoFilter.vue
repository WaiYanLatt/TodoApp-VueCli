<script>
export default {
    emits: ["setFilter"],
    props: {
        filterStatus: {
            type: String,
            required: true,
        },
        totalTodos : {
            type  : Number,
            required : true,
        }
    },
};
</script>
<template>
    <div class="border">
        <h3 class="text">({{ totalTodos }}) items left</h3>
        <div class="filter">
            <button class="btn2" @click="$emit('setFilter', 'all')" :class="{ selected: filterStatus === 'all' }">
                All
            </button>
            <button class="btn2" @click="$emit('setFilter', 'active')" :class="{ selected: filterStatus === 'active' }">
                Active
            </button>
            <button class="btn2" @click="$emit('setFilter', 'completed')" :class="{ selected: filterStatus === 'completed' }">
                Completed
            </button>
        </div>
    </div>
</template>
<style scoped>
.border {
    display: flex;
    align-items: center;
    justify-content: space-between;
    border: 1px solid white;
    border-left: 0px;
    border-right: 0px;
    margin-top: 30px;
}

.btn2 {
    background-color: white;
    border: 0px;
    margin-right: 10px;
    padding: 10px;
    font-weight: bold;
    border-radius: 5px;
    font-size: 1rem;
    cursor: pointer;
}

.filter button.selected {
    background-color: greenyellow;
    color: white;
}
.text{
    color: white;
}
</style>
