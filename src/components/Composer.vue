<template>
    <form @submit.prevent="$emit('onEnter')" >
      <input :value="modelValue" @keydown="$emit('update:modelValue', $event.target.value)" type="text" placeholder="Type and hit enter..." class="composer__input focus: outline-none focus: ring-0" />
    </form>
</template>
<script>
export default {
    props:{
        modelValue: {
            type: String,
            required: true,
        }
    }
}
</script>