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
        transform: translateY(-22%);
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
</style>