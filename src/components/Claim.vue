<template>
  <div class="claimWrapper">
    <h1 class="claim">SPACER</h1>
    <p class="subclaim">
      Lorem ipsum dolor sit amet, consectetur adipisicing elit. Itaque magni sequi temporibus.    Beatae, obcaecati, possimus.
    </p>
    <p class="subclaim">
      Lorem ipsum dolor sit amet, consectetur adipisicing elit.
    </p>
  </div>
</template>

<script>
  export default {
    name: 'Claim',
  };
</script>

<style lang="scss" scoper>
  .claimWrapper{
    display:flex;
    text-align: center;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .claim{
    font-size:50px;
    margin:0;

    @media(min-width: 768px){
    font-size:80px;
    }

    @media(min-width: 1024px){
      font-size:100px;
    }

  }

  .subclaim{
    font-size:13px;
    margin: 20px 0 0 0;

    @media(min-width: 768px){
      font-size:17px;
      line-height: 1.5;
      width:500px;
      letter-spacing: 1px;
    }
  }
</style>
