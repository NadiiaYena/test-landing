<script>
import FormBlock from './components/Form/FormBlock.vue';
import List from './components/ListBlock/List.vue';
import SliderBlock from './components/Slider/Slider.vue';

export default {
    name: 'App',
    components: {
        SliderBlock,
        FormBlock,
        List,
    }
}

</script>

<template>
    <div class="app">
        <slider-block/>
        <form-block/>
        <list/>
    </div>

</template>

<style scoped>
.app{
    margin: 0;
    padding: 0;

}

</style>
