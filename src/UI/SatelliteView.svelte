<script>
    import { isEmpty } from "../helpers/validation.js";

    let latitude = "";
    let longitude = "";
    let rDate = "";
    let pDate = "";

    const baseUrl = "http://localhost:8080/satellite?";
    let recentUrl, pastUrl;

    let isFormValid = false;
    let showImages = false;

    $: latitudeValid = !isEmpty(latitude);
    $: longitudevalid = !isEmpty(longitude);
    $: rDatevalid = !isEmpty(rDate);
    $: pDatevalid = !isEmpty(pDate);
    $: isFormValid =
        latitudeValid && longitudevalid && rDatevalid && pDatevalid;

    const submitForm = () => {
        if (isFormValid) {
            recentUrl = `${baseUrl}latitude=${latitude}&longitude=${longitude}&date=${rDate}`;
            pastUrl = `${baseUrl}latitude=${latitude}&longitude=${longitude}&date=${pDate}`;
            showImages = true;
        }
    };
</script>

<div class="compare-container">
    <h1>Want to compare the satellite images of a particular regin?</h1>
    <button> Proceed</button>
</div>
<div class="main-compare-container">
    <div class="form">
        <div class="inputs">
            <input
                type="Number"
                class="latitude"
                on:input={(event) => (latitude = event.target.value)}
                placeholder="Latitude"
            />
            <input
                type="Number"
                class="Longitude"
                on:input={(event) => (longitude = event.target.value)}
                placeholder="Longitude"
            />
            <input
                type="date"
                class="recent-date"
                on:input={(event) => (rDate = event.target.value)}
                placeholder="Recent date"
            />
            <input
                type="date"
                class="past-date"
                on:input={(event) => (pDate = event.target.value)}
                placeholder="Past date"
            />
        </div>
        <input type="submit" on:click={submitForm} class="submit" />
    </div>
    <div class="compare-results">
        <div class="results">
            {#if showImages}
                <div class="past-result">
                    <img src={pastUrl} alt="Past" />
                    <h3>Date:</h3>
                </div>
                <div class="recent-result">
                    <img src={recentUrl} alt="Recent" />
                    <h3>Date:</h3>
                </div>
            {/if}
        </div>
    </div>
</div>

<style>
    .compare-container {
        height: 100vh;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }

    .compare-container h1 {
        text-align: center;
    }

    .compare-container button {
        outline: none;
        padding: 7px 10px;
        margin: 0;
        background-color: #10316b;
        color: #fff;
        font-size: 18px;
        border: none;
        cursor: pointer;
    }

    .main-compare-container {
        height: 100vh;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }

    .main-compare-container .form {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        margin-top: 30px;
        padding: 15px 20px;
        border-radius: 20px;
        border: 1px solid rgba(0, 0, 0, 0.5);
    }

    .main-compare-container .form input {
        padding: 5px 10px;
        border-radius: 10px;
        outline: none;
        border: 1px solid #000;
    }

    .main-compare-container .form input[type="submit"] {
        outline: none;
        padding: 7px 10px;
        margin-top: 10px;
        background-color: #10316b;
        color: #fff;
        font-size: 18px;
        border: none;
        cursor: pointer;
    }

    .compare-results {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }

    .results {
        display: flex;
        justify-content: center;
        align-items: center;
        margin-top: 30px;
    }

    .past-result,
    .recent-result {
        width: 400px;
        height: 400px;
        margin: 20px;
        text-align: center;
    }

    .past-result img,
    .recent-result img {
        height: 100%;
        width: 100%;
    }
</style>
