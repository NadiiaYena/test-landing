<template>
    <div class="list-wrap">
        <div class="sorting">
            <label>
                <input type="radio" value="sortTitle" v-model="selectedOption" @change="handleRadioChange"/>  
                відсортувати блоки за заголовком відповідно до алфавітного порядку</label>
            <label>
                <input type="radio" value="imageLeft" v-model="selectedOption" @change="handleRadioChange"/> 
                вивести всі блоки у форматі "зображення - зліва, текст - справа"</label>
            <label>
                <input type="radio" value="notSort" v-model="selectedOption" @change="handleRadioChange"/>
                вивести всі блоки у форматі "зображення - зліва, текст - справа" і навпаки в шаховому порядку</label>
        </div>
        <ul class="list">
            <li v-for="(item, index) in sortData" :key="index" class="list-item">
                <list-block :item="item" :index="index" :selectedOption="selectedOption"/>
            </li>
       </ul>
    </div>
</template>

<script>
import ListBlock from './ListBlock.vue';

export default {
    name: 'List',
    components: {
        ListBlock
    },
    data(){
        return {
            data: null,
            images: null,
            selectedOption: '',
        }
     
    },
    created(){
 console.log('created list')
    },
    mounted(){
        console.log('mounted list')
        fetch('https://api.themoviedb.org/3/discover/movie?api_key=3685d3eb8695f087227e0ee980f3ae4d&language=en-US&sort_by=popularity.desc&include_adult=false&include_video=false&page=1'
           )
           .then(response => {
            if (!response.ok) {
            throw new Error('Network response was not ok ' + response.statusText);
            }
            return response.json();
        })
        .then(data => {
            console.log(data);
            this.data = data.results;
        })
        .catch(error => {
            console.error('There has been a problem with your fetch operation:', error);
        });


    },
    computed:{
           sortData(){
            if(this.selectedOption === 'sortTitle'){
                return [...this.data].sort((a, b) => a.original_title.localeCompare(b.original_title));
            }
             else {
                return this.data
            }
            
           }
    },
    methods: {

    }



}
</script>

<style>
.list-wrap {
    display: flex;
    flex-direction: column;
    gap: 67px;
    justify-content: center;
    align-items: center;


}
.sorting {
    display: flex;
    flex-direction: column;
    max-width: fit-content;
    gap: 26px;
    padding-left: 10px;
}
label {
    display: flex;
    flex-direction: row;
    gap: 10px;
    justify-content: flex-start;
    align-items: center;

}
.list {
    list-style: none;
    display: flex;
    flex-direction: column;
    gap: 20px;
    margin: 0;
    padding: 0;
}
.list-item{
    display: flex;
    
}
</style>