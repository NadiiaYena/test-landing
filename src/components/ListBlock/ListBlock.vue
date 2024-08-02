<template>
  <div class="listBlock-wrap" :class="{ revers: imagesLeft }" ref="myElement">
    <div class="image-wrap">
      <img
        :src="`https://image.tmdb.org/t/p/w185_and_h278_bestv2/${item.poster_path}`"
        :alt="item.title"
      />
    </div>
    <div class="description">
      <h3>{{ item.original_title }}</h3>
      <p>{{ item.overview }}</p>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  name: "ListBlock",
  data() {
    return {
      imagesLeft: false,
    };
  },
  props: {
    item: {
      type: Object,
      required: true,
    },
    index: {
      type: Number,
      required: true,
    },
    selectedOption: {
      type: String,
    },
  },

  mounted() {
    // console.log(this.item, this.index)
    this.checkStyle();
  },
  computed: {},
  watch: {
    selectedOption(newValue) {
      this.checkStyle();
    },
  },
  methods: {
    checkStyle() {
      // console.log(this.selectedOption)
      if (this.selectedOption === "imageLeft") {
        console.log("remove revers");
        this.$refs.myElement.classList.remove("revers");
      } else {
       
        console.log('checkStyle else')
        if (this.index % 2 !== 0) {
          this.$refs.myElement.classList.add("revers");
        } 
      }
    },
  },
};
</script>

<style scoped>
.listBlock-wrap {
  max-width: 1020px;
  /* height: 324px; */
  padding: 27px 40px 33px 40px;
  border: 1px #000;
  background: #c4c4c4;
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  align-items: center;
  gap: 46px;
}
.revers {
  max-width: 1020px;
  height: 324px;
  padding: 27px 40px 33px 40px;
  border: 1px #000;
  background: #c4c4c4;
  display: flex;
  flex-direction: row-reverse;
  justify-content: space-between;
  align-items: center;
  gap: 46px;
}

.image-wrap {
  display: flex;
  justify-content: center;
  align-items: center;

  height: 264px;
}
.description {
  display: flex;
  flex-direction: column;
  gap: 21px;
  /* height: 130px; */
  
}
</style>
