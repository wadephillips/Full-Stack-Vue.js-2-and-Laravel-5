<template>
    <div class="image-carousel">
        <img :src="image">
        <div class="controls">
            <carousel-control
                    dir="left"
                    @change-image="changeImage"
            ></carousel-control>
            <carousel-control
                    dir="right"
                    @change-image="changeImage"
            ></carousel-control>
        </div>
    </div>
</template>

<script>
  export default {
    props: ['images'],
    data() {
      return {
        index: 0
      }
    },
    computed: {
      image() {
        return this.images[this.index];
      }
    },
    methods: {
      changeImage(val) {
        let newVal = this.index + parseInt(val);
        if (newVal < 0) {
          this.index = this.images.length - 1;
        } else if (newVal === this.images.length) {
          this.index = 0;
        } else {
          this.index = newVal;
        }
      },
      components: {
        'carousel-control': {
          template: `<i :class="classes" @click="clicked"></i>`,
          props: ['dir'],
          computed: {
            classes() {
              return 'carousel-control fa fa-2x fa-chevron-' + this.dir;
            }
          },
          methods: {
            clicked() {
              this.$emit('change-image', this.dir === 'left' ? -1 : 1);
            }
          }
        }
      }
    }
  }
</script>

<style scoped>

</style>