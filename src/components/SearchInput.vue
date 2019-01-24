<template>
    <input id="search" type="text" name="search" :value="value" @input="handleChange" :class="{dark}">
</template>

<script>
  export default {
    name: 'SearchInput',
    props: {
      value: {
        type: String,
        required: true,
      },
      dark:{
        type: Boolean,
        default: false,
      },
    },
    methods: {
      handleChange(e){
        this.$emit('input', e.target.value)
      }
    }
  };
</script>

<style lang="scss" scoped>

    input{
      margin-top:50px;
      display: flex;
      width:250px;
      border:0;
      color:white;
      text-align: center;
      font-size:18px;
      border-bottom:1px solid white;
      height:30px;
      background: none;
      &:focus{
        outline:none;
      }
    }

  .dark{
    color: #1e3d4a;
    border-bottom: 1px solid #1e3d4a;
  }

  .dark:focus{
    outline:none;
  }
</style>
