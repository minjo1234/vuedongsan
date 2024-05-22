<template>
  <div class="discount">
    <h4>지금 결제하면 {{discount_rate}}% 할인 </h4>
  </div>
</template>

<script>
export default {
  name: 'Discount',
  data(){
    return {
      discount_rate: 30
    }
  },
  methods(){
  },

  mounted() {
    // clearInterval를 지정하고 싶은경우 setInterval 구문을 변수로 선언해주고 clearInterval을 조건문을 선언해서
    // 멈춰주면 된다.
     var timer = setInterval(()=>{
       this.discount_rate -= 1;
       if(this.discount_rate == 0){
         clearInterval(timer);
       }
     }, 1000 )
  }
};
</script>

<style></style>
