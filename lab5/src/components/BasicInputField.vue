<template>
    <div class="field">
        <input
        v-bind:value="value"
        v-on:input="$emit('input', $event.target.value)"
        >
    </div>
</template>

<script>
export default{
        name: "BasicInputField",
        props: ['value']
}
</script>


