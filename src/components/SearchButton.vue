<template>
  <button class=form-button aria-label=search type=submit>
    <slot></slot>
  </button>
</template>


<style scoped>
.form-button {
  border-radius: 0 10px 10px 0;
  padding-right: 10px;
}
</style>