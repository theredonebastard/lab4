<template>
  <div>
    <div class="body" v-show="show">
      <slot #default></slot>
      <button type="button" aria-label="Close" v-show="dismissible" @click.prevent="onClose"><span aria-hidden="true">&times;</span></button>
    </div>
    <div class="footer">
      <slot name="activator" :on="on"></slot>
    </div>
  </div>
</template>

<script>
  export default {
    name: "BAlert",
    model:{
      prop: 'show',
      event: 'close'
    },
    props: {
      show:{
        type:[Boolean,Number],
        default:0
      },
      variant:{
        type:String,
        default:"danger"
      },
      dismissible:{
        type:Boolean,
        default:false
      }
    },
    data(){
      return{
        countdown:this.show
      }
    },
    methods: {
      onClose: function() {
        this.$emit('close');
      },
      on:function(){
        this.$emit('start');
      }
    },
    watch:{
      show: function(){
        this.countdown = this.show;
      },
      countdown:function(){
        if(this.countdown>0){
          setTimeout(()=>{
            this.countdown--;
            this.$emit('dismiss-countdown',this.countdown);
          }, 1000);
        }
        else{
          this.$emit('close');
        }
      }
    }
  }
</script>