<template>
    <div class="task" :class="stateClass" @click="$emit('taskStateChanged', task)">
        <span @click.stop="$emit('taskDeleted', task)" class="close">x</span>
        <p> {{task.name}}</p>
    </div>
</template>

<script>
export default {
    props: {
        task: {type: Object, required: true}
    },
    computed: {
        stateClass(){
            return {
                pending: this.task.pending,
                done: !this.task.pending
            }
        }
    }
}
</script>

<style>

.task {
    position: relative;
    box-sizing: border-box;
    width: 350px;
    height: 150px;
    padding: 10px;
    border-radius: 8px;
    font-size: 2rem;
    font-weight: 300;
    cursor: pointer;
    user-select: none;
    display: flex;
    justify-content: center;
    align-items: center;
}

.pending {
    border-left: 12px solid #930000;
    background-color:  #c40000;
}

.done {
    color: #DDD;
    border-left: 12px solid rgb(0, 82, 38);
    background-color: rgb(1, 136, 64);
    text-decoration: line-through;

}

.pending .close {
    background-color: #930000;
}

.done .close {
    background-color: rgb(0, 82, 38);
}

.close {
    position: absolute;
    right: 10px;
    top:10px;
    font-size: 0.9rem;
    font-weight: 600;
    height: 20px;
    width: 20px;
    border-radius: 10px;
    justify-content: center;
    display: flex;

}

</style>
