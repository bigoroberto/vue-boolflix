
<template>
    <header class="d-flex justify-content-between align-items-center ps-4 pe-4 pt-2 pb-2">
        <h1 class="pe-2">BOOLFLIX</h1>
        <div class="d-flex">
            <!-- barra di ricerca -->
            <div>
                <input type="text"
                v-model.trim= "findMovie"
                placeholder="Cerca film e serie tv..."
                @keyup.enter="$emit('searchMovie',{text:findMovie, type:'all'})"
                >
            </div>
            <!-- bottoni -->
            <!-- <div>
                <button
                @click.prevent="$emit('searchMovie',{text:findMovie, type:'movie'})"
                >Cerca film</button>
            </div>
            <div>
                <button
                @click.prevent="$emit('searchMovie',{text:findMovie, type:'tv'})"
                >Cerca serie tv</button>
            </div> -->

            <div>
                <button
                class="btn"
                @click.prevent="$emit('searchMovie',{text:findMovie, type:'all'})"
                >Cerca</button>
            </div>
            <div>
                <button
                 class="btn"
                @click.prevent="resetAll()"
                >Reset</button>
            </div>
            <div class="icon">
                <i class="fas fa-search" @click.prevent="$emit('searchMovie',{text:findMovie, type:'all'})"></i>
            </div>
            <div class="icon">
                <i class="fas fa-undo-alt" @click.prevent="resetAll()"></i>
            </div>
        </div>

    </header>
</template>

<script>
export default {
    name:'Header',
    data(){
        return {
            findMovie: ""
        }
    },
    props:{
        setDefault: Function
    },
    methods:{
        resetAll(){
            this.findMovie="";//svuoto il campo di ricerca
            this.setDefault();//richiamo la funzione setDefault passata come props
        }
    }
}
</script>

<style lang="scss" scoped>
header{
    background-color: #000;
    background-image: linear-gradient(#000,#272727);
    h1{
        color: #D10015;
        margin: 0;
    }
    input{
        width: 400px;
    }
    .btn{
        background-color: #8d8d8d;
        padding: 2px 10px;
        font-weight: 700;
        color: #ffffff;
        margin-left: 15px;
    }
    .icon{
        display: none;
        color: white;
        cursor: pointer;
    }
}
@media screen and (max-width: 800px){
    header{
        input{
            width: 300px;
        }
    }
}
@media screen and (max-width: 700px){
    header{
        input{
            width: 100%;
            &::placeholder{
                font-size: 12px;
            }
        }
        .btn{
            display: none;
        }
        .icon{
            display: block;
            margin-left: 10px;
            margin-top: 3px;
        }
    }
}
</style>