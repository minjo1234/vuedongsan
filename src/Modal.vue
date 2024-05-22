<template>
  <div class="black-bg" v-show="model_state">
    <div class="white-bg">
      <img :src="onerooms[click_Number].image" />
      <h4>{{ onerooms[click_Number].title }}</h4>
      <p>{{ onerooms[click_Number].content }}</p>
      <input v-model.number="month">
      <input type="range" min="1" max="12">
      <p>{{month}}개월 선택함 : {{ onerooms[click_Number].price * month}}</p>
      <button @click=send()>닫기</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Modal',
  data() {
    return {
      month : 1,
    }
  },
  watch:{
    month(input_data){
      console.log(input_data)
      if (input_data >= 13){
        alert('13이상 입력하지 마셈')
        this.month = 12
      } else if(typeof (input_data) == 'string' && (input_data) != ''){
        alert('글자 입력 금지!')
        this.month = 1
      } else if(input_data == 2){
        alert('최소 3개월 이상부터 결제가능합니다')
        this.month = 3
      }
    }
  },
  props : {
    onerooms: Array,
    click_Number: Number,
    model_state: Boolean,
  },
  methods :{
    send(){
      this.$emit('modal_close');
    }
  }


};
</script>

<style></style>
