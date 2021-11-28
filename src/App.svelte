<script>
    import Header from "./UI/Header.svelte";
    import ApodView from "./UI/ApodView.svelte";
    import SearchView from "./UI/SearchView.svelte";

    let path;

    function setRoute(event) {
        path = event.detail;
    }
</script>

<Header on:select={setRoute}/>
<main>
    {#if path === 0}
        <ApodView />
    {:else if path === 1}
        <SearchView />
    {/if}
</main>
