<script>
    import SearchElement from "./SearchElement.svelte";
    import { isEmpty } from "../helpers/validation.js";

    const baseUrl = "http://localhost:8080/search?q=";
    let url;
    let data;
    let pageData;
    let fetched = false;
    let hasValidData = true;

    let keyword = "";

    $: keywordValid = !isEmpty(keyword);
    $: hasValidData = (data != 0);
    // $: console.log(keyword);

    const fetchData = () => {
        if (keywordValid) {
            url = baseUrl + keyword.trim();
            axios.get(url).then((response) => {
                if (response.data == 0) {
                    data = [];
                }
                else {
                    data = response.data;
                }
                pageData = data.slice(0, 8);
                fetched = true;
                console.log(pageData);
            });
        }
    };
</script>

<div class="search">
    <div class="search-container">
        <input
            type="text"
            placeholder="Search.."
            on:input={(event) => (keyword = event.target.value)}
        />
        <button on:click={fetchData}><i class="fas fa-search" /></button>
        {#if !keywordValid}
            <p class="error">Please enter valid data!</p>
        {/if}
    </div>
</div>
<div class="search-results">
    {#if (fetched && hasValidData)}
        {#each pageData as element (element.href)}
            <SearchElement
                title={element.data[0].title}
                imageUrl={element.links[0].href}
            />
        {/each}
    {:else if !hasValidData}
        <h2>No Data Found!</h2>
    {/if}
</div>

<style>
    .error {
        color: red;
        display: flex;
        justify-content: center;
    }

    .search {
        display: flex;
        justify-content: center;
        align-items: center;
        position: relative;
        height: 20vh;
    }

    .search .search-container input {
        outline: none;
        padding: 5px 10px;
        margin: 0;
        font-size: 18px;
    }
    .search .search-container button {
        outline: none;
        padding: 7px 10px;
        margin: 0;
        background-color: #10316b;
        color: #fff;
        font-size: 18px;
        border: none;
        cursor: pointer;
    }

    .search-results {
        display: flex;
        align-items: center;
        justify-content: center;
        flex-wrap: wrap;
        width: 100vw;
    }
</style>
