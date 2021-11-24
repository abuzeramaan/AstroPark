<script>
</script>

<nav class="navbar ">
    <h2 class="navbar-logo">Astro Park</h2>
    <ul class="navbar-list">
        <li>Home</li>
        <li>Library</li>
        <li>Geo Satelite</li>
        <li>About</li>
    </ul>
</nav>

<style>
    nav {
        display: flex;
        justify-content: space-between;
        align-items: center;
        text-align: center;
        background-color: #10316b;
        color: #ececeb;
    }

    nav ul {
        list-style-type: none;
        display: flex;
        margin: 0 15px;
        height: 100%;
    }

    nav ul li {
        height: 100%;
        margin: 0 10px;
        padding: 15px 0px;;
        font-size: 25px;
    }

    nav ul li:hover {
        color: #ffffff;
        cursor: pointer;
        transform: scale(110%);
    }

    nav h2 {
        padding: 0 15px;
    }
</style>
