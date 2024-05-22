<template>
  <div>
    <img :src="oneroom.image" class="room-img" />
    <h4 @click="send">{{oneroom.title}}</h4>
    <p>{{ oneroom.price }}원</p>
    <span>{{ oneroom.content }}</span>
  </div>
</template>


<script>
export default {
    name : 'Card',
    props : {
      oneroom : Object,
    },
  methods :{
      send(){
        this.$emit('open_modal' , this.oneroom.id)
      }
  }
}
</script>

<style scoped>

</style>