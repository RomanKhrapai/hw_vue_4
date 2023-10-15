<template>
    <input class=form-input type=text required autocomplete=off :value="value" placeholder='Введіть число' />
</template>

<script>
export default {
    props: ["value"],
};
</script>

<style >
.form-input {
    border-radius: 10px 0 0 10px;
    padding-left: 20px;
    border-right: none;
}
</style>