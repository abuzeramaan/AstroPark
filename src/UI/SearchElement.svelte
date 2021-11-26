<script>
    export let imageUrl;
    export let title;
    
    // console.log(imageUrl, title);
</script>

<div class="result">
    <img
        src="{imageUrl}"
        alt="{title}"
    />
    <h3>{title}</h3>
</div>

<style>
    .result {
        height: 300px;
        width: 400px;
        margin: 30px;
        position: relative;
    }

    .result img {
        height: 100%;
        width: 100%;
    }

    .result h3 {
        position: absolute;
        bottom: -5%;
        color: #fff;
        padding: 0 15px 15px 15px;
        background-color: rgba(0, 0, 0, 0.5);
        width: 100%;
    }
</style>
