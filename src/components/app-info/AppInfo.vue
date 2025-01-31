<template >
    <div class="app-info">
        <h2>Barcha kinolar : {{ addMovieCount }}</h2>
        <h4>Ko'rilgan kinolar : {{ favMovieCount }} </h4>
    </div>
</template>
<script>
export default {
    props: {
        addMovieCount: {
            type: Number,
            required: true
        },
        favMovieCount: {
            type: Number,
            required: true
        }
    }
}
</script>
<style scoped>
    
    .app-info{
        background-color: #f4f4f4;
        padding: 1rem;
        border-radius: 5px;
        margin-bottom: 1rem;
    }
    h2{
        font-size: 1.5rem;
        margin-bottom: 1rem;
        font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
    }
    h4{
        font-size: 1rem;
        font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
        margin-bottom: 1rem;
    }

</style>