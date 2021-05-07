<template>

    <div id="pokemon">
        <div class='card'>
        <div class='card-image'>
            <figure>
                <img :src="currentImg" alt="">
            </figure>
        </div>
        <div class='card-content'>
            <div class='media'>
            <div class='media-content'>
                <p class='title is-4'>{{ id+1 }} - {{name | upper}}</p>
                <div class='' v-for="(type,index) in pokemon.types" :key='index'>
                    <p class='subtitle is-6'>{{type.type.name}}</p>      
                </div>
                
            </div>    
            </div>

            <div class='content'>
                <button class='button is-medium is-fullwidth' @click='mudarSprite'>Change</button>
            </div>
        </div>
        </div>




    </div>

</template>

<script>
import axios from 'axios';
export default {
    created: function(){
        axios.get(this.url).then(res=>{
            this.pokemon.types = res.data.types;
            this.pokemon.front_sprite = res.data.sprites.front_default;
            this.pokemon.back_sprite = res.data.sprites.back_default;
            this.currentImg = this.pokemon.front_sprite
            console.log(this.pokemon)
        })
    },
    data(){
        return {
            isFront:true,
            currentImg:'',
            pokemon:{
                types:'',
                front_sprite:'',
                back_sprite:'',
            }
        }
    },
    props:{
        id: Number,
        name: String,
        url: String
    },
    filters:{
        upper:function(value){
            var newName = value.charAt(0).toUpperCase() + value.substr(1)
            return newName
        }
    },
    methods:{
        mudarSprite:function(){
            if(this.isFront){
                this.isFront=false;
                this.currentImg=this.pokemon.back_sprite
            }else{
                this.isFront=true;
                this.currentImg=this.pokemon.front_sprite
            }
        }
    }
}
</script>

<style >
    #pokemon{
        margin-top:2%;
    }
</style>