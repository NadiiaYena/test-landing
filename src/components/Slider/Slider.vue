<template>
  <div class="slider-wrap">
    <ul class="slider-list">
      <li
        class="slide"
        id="slide-0"
        :class="getClassForSlide(0)"
      >
        <div class="image-1">
           <p class="slogan">LOREM IPSUM DOLOR SIT AMET</p>
          
            <span class="title-line-1">LOREM IPSUM</span>
            <span class="title-line-2">LOREM IPSUM DOLOR — </span>
            <span class="title-line-3">LOREM</span>
            <span class="title-line-4">IPSUM ! </span>
      
          <span class="slogan-2">LOREM IPSUM DOLOR SIT AMET, CONSECTETUR ADIPISCING ELIT</span>
          <img src="/src/icons/Dawn.png" class="img-star"/>
          <img src="/src/icons/Ellipse_7.png" class="img-elips-grey-1"/>
          <img src="/src/icons/Group_37.png" class="img-dog"/>
          <img
            src="/src/icons/cursor_arrow.png"
            class="arrow-cursor"
            @click="nextSlide()"
          />
        </div>
        <span class="numberPage">{{ currentIndex + 1 }} / {{ slides }}</span>

      </li>
      <li
        class="slide"
        id="slide-1"
         :class="getClassForSlide(1)"
      >
        <div class="image-2">
            <p class="slogan">LOREM IPSUM DOLOR SIT AMET</p>
          <h1 class="title">
            <span class="title-line-1">LOREM IPSUM</span>
            <span class="title-line-2">LOREM IPSUM DOLOR — </span>
            <span class="title-line-3">LOREM</span>
            <span class="title-line-4">IPSUM ! </span>
        </h1>
          <span class="slogan-2">LOREM IPSUM DOLOR SIT AMET, CONSECTETUR ADIPISCING ELIT</span>
          <img src="/src/icons/Dawn.png" class="img-star"/>
          <img src="/src/icons/Ellipse_7.png" class="img-elips-grey-1"/>
            <img src="/src/icons/Group_37.png" class="img-dog"/>
          <img
            src="/src/icons/cursor_arrow.png"
            class="arrow-cursor"
            @click="nextSlide()"
          />
        </div>
        <span class="numberPage">{{ currentIndex + 1  }} / {{ slides }}</span>
      </li>
      <li
        class="slide"
        id="slide-2"
        :class="getClassForSlide(2)"
      >
        <div class="image-3">
            <p class="slogan">LOREM IPSUM DOLOR SIT AMET</p>
          <h1 class="title">
            <span class="title-line-1">LOREM IPSUM</span>
            <span class="title-line-2">LOREM IPSUM DOLOR — </span>
            <span class="title-line-3">LOREM</span>
            <span class="title-line-4">IPSUM ! </span>
        </h1>
          <span class="slogan-2">LOREM IPSUM DOLOR SIT AMET, CONSECTETUR ADIPISCING ELIT</span>
          <img src="/src/icons/Dawn.png" class="img-star"/>
          <img src="/src/icons/Ellipse_7.png" class="img-elips-grey-1"/>
            <img src="/src/icons/Group_37.png" class="img-dog"/>
          <img
            src="/src/icons/cursor_arrow.png"
            class="arrow-cursor"
            @click="nextSlide()"
          />
        </div>
        <span class="numberPage">{{ currentIndex +1  }} / {{ slides }}</span>

      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "SliderBlock",
  data() {
    return {
      currentIndex: 0,
      slides: 3,
    };
  },
  methods: {
    nextSlide() {
        const currentSlide = document.querySelector(`.slide.one`);
        currentSlide.style.transition = "transform 0.5s ease";
      currentSlide.style.transform = "translateX(-100%)";
      
      setTimeout(() => {
        this.currentIndex = (this.currentIndex + 1) % this.slides;
        currentSlide.style.transition = "none";
        currentSlide.style.transform = "translateX(0)";
      }, 500);
    },    
    
    getClassForSlide(index) {
      const classes = ["one", "two", "three"];
      const offset = (index - this.currentIndex + this.slides) % this.slides;
      return classes[offset];
    },
  },
};
</script>

<style scoped>
.slider-wrap {
  position: relative;
  height: 708px;
  width: 100vw;
  overflow: hidden;
}

.slider-list {
  display: flex;
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
  list-style: none;
  position: relative;
}

.slide {
  width: 93%;
  height: 100%;
  position: relative;
  /* transition: transform 0.5s ease; */
  position: absolute;
  background-color: rgb(31, 78, 119);
}

.one,
.two,
.three {
  border: 1px solid #000;
  border-top-right-radius: 50px;
  border-bottom-right-radius: 50px;
  height: 100%;
  overflow: hidden;
  
}
.image-1 {
    background-color: #027D84;
    height: 100%;
}
.image-2{
    background-color: rgb(163, 127, 255);
    height: 100%;

}
.image-3{
    background-color: rgb(24, 8, 247);
    height: 100%;

}

.one {
  width: 93%;
  z-index: 3;
}

.two {
  width: 97%;
  z-index: 2;
}

.three {
  width: 100%;
  z-index: 1;
 

}
.two::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(134, 133, 133, 0.424); 
  z-index: 1; 
}
.three::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgb(103, 102, 102); 
  z-index: 1; 
}

.arrow-cursor {
  position: absolute;
  cursor: pointer;
  top: 50%;
  right: 50px;
  transform: translateY(-50%);
}

.img-star,
.img-elips,
.img-dog,
.img-elips-grey-1,
.img-elips-grey-2{
 position: absolute;
}
.img-star{
    left: 0;
    top: 357px;
}
.img-elips-grey-1{
top: 0;
left: 110px;
z-index: 1;

}
.img-dog{
    right: 60px;
    top: 50px;
    
}
/* .title{
   
    margin: 0;
    padding: 0;
} */
.title-line-1{
    position: absolute;
    z-index: 2;
font-size: 60px;
font-weight: 700;
line-height: 64px;
/* text-align: left; */
color: #fff;
top: 116px;
left: 152px;


}
.title-line-2{
    position: absolute;
    z-index: 2;

font-size: 60px;
font-weight: 400;
line-height: 70px;
/* text-align: left; */
color: #fff;
top: 185px;
left: 193px;

text-shadow: 
        1px 1px 0 #000,  
        -1px -1px 0 #000,
        1px -1px 0 #000,
        -1px 1px 0 #000;
    

}
.title-line-3{
    top: 255px;
    left: 442px;

}
.title-line-4{

    top: 327px;
    left: 293px;
}

.title-line-3,
.title-line-4{
    position: absolute;
    z-index: 2;

font-size: 60px;
font-weight: 400;
line-height: 70px;
/* text-align: left; */
color: #fff;
}

.slogan{
    position: absolute;
font-size: 18px;
font-weight: 500;
line-height: 21.09px;
text-align: center;
color: #fff;
z-index: 2;
top: 17px;
left: 252px;


}
.slogan-2{
font-size: 15px;
font-weight: 500;
line-height: 22.5px;
text-align: left;
color: #fff;
position: absolute;
z-index: 2;
top: 437px;
left: 436px;
width: 278px;
}
.numberPage {
    color: #fff;
    border: 1px solid #fff;
    border-radius: 60%;
    padding: 10px 32px;
    position: absolute;
    bottom: 33px;
    left: 21px;
    z-index: 3;
    display: none;
}

@media screen and (max-width: 1250px){
    .slogan-2{
        left: auto;
        right: 40px;
        top: 570px
    }
}
@media screen and (max-width: 915px){
    .title-line-2{
        left: 50px;
    }
    /* .slogan-2{
        left: 550px;
        top: 570px
    } */

}

@media screen and (max-width: 768px){
    .numberPage {
        display: block;
    }
    .slider-wrap {
  height: 900px;
}
.img-star{
    left: -49px;
    top: 242px;
}

.slogan{
top: 12px;
left: 185px;


}
.title-line-1,
.title-line-2,
.title-line-3,
.title-line-4{
    font-size: 40px;
    line-height: 52px;
}
.title-line-1{
    top: 107px;
    left: 82px;
}
.title-line-2{
    left: 125px;
    top: 164px;

    text-shadow: none;

}
.title-line-3{
    top: 216px;
    left: 318px;

}
.title-line-4{
    top: 268px;
    left: 196px;

}

.img-dog{
    right: 90px;
    bottom: -18px;
    scale: 76%;
    top: auto;
}
.arrow-cursor {
  position: absolute;
  cursor: pointer;
  top: 50%;
  right: 50px;
  transform: translateY(0%);




}
.slogan-2{
font-size: 15px;
font-weight: 500;
line-height: 22.5px;
text-align: left;
color: #fff;
position: absolute;
z-index: 2;
top: 319px;
left: 368px;
width: 278px;
}

}
</style>
