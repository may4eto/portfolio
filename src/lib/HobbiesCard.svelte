<script>
    export let data
</script>

<div class="card">
    <h2>Hobbies</h2>
    <div class="card-grid">
        {#each data.hobbies as hobby }
            <div class="hobby-card">
                <img class="img" src="images/{hobby.image}" alt="" />
                <h3>{hobby.name}</h3>
                <p>{hobby.description}</p>
            </div>
        {/each}
    </div>
</div>

<style>
    .card {
        margin-top: -50%;
    }
    .card h3 {
        font-size: 18px;
        margin: 8px 0;
        font-weight: 600;
    }
    .card p {
        margin: 0;
    }
    .card .card-grid .hobby-card:not(:last-child) {
        margin-bottom: 32px;
    }
    .card .card-grid .hobby-card:last-child {
        margin-bottom: 24px;
    }
    .card .card-grid .hobby-card .img {
        width: 100%;
        height: 140px;
        object-fit: cover;
        border-radius: 12px;
    }
    .card .card-grid .hobby-card p {
        color: var(--text-color-grey);
        font-size: 16px;
    }
    @media (max-width: 1024px) {
        .card {
            margin-top: -53%;
        }
    }
    @media (max-width: 1007px) {
        .card .card-grid {
            padding-bottom: 0px;
        }
    }
    @media (max-width: 986px) {
        .card {
            margin-top: -33%;
        }
        .card .card-grid {
            padding-bottom: 48px;
        }
    }
    @media (max-width: 986px) {
        .card {
            margin-top: -28%;
        }
        .card .card-grid {
            padding-bottom: 32px;
        }
    }
    @media(max-width: 950px) {
        .card {
            margin-top: 0%;
        }
        .card .card-grid .hobby-card .img {
            width: 100%;
            height: 280px;
        }
    }
</style>