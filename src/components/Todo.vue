<template>
    <!-- Todo start -->
    <div @click="$emit('onToggle',todo)" class="todo hover: bg-gray-100" :class="{
      'todo--done':todo.done
      }" >
      <div class="todo__status-dot"></div>
      <div>
        <p class="todo__content">{{todo.task}}</p>
        <small class="todo__time"> {{todo.time}} </small>
      </div>
    </div>
    <!-- Todo end -->
</template>
<script>
export default {
    props:["todo"],
}
</script>