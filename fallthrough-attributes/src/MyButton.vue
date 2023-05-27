<!-- Disabling attribute inheritance by inheritAttrs: false -->
<script>
export default {
  inheritAttrs: false,
};
</script>

<script setup></script>

<template>
  <div class="btn-wrapper">
    <!-- You can access these fallthrough attributes manually via $attrs -->
    <!-- $attrs is the object includes all attributes that are not declared
      by the component's props or emits
    -->
    <!-- v-bind without an argument binds all the properties of an object -->
    <button class="btn" v-bind="$attrs">button</button>
  </div>
</template>

<style>
.btn-wrapper {
  margin: 2px;
}

.btn {
  padding: 2px 4px;
  cursor: pointer;
}
</style>
