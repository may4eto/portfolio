<script>
    export let data
</script>

<div class="card profile">
    <img src="images/profile-image.jpg" alt="" />
    <div class="text">
        <div class="header">
            <div class="name">
                <h1>{data.name}</h1>
                <p>{data.role}</p>
            </div>
            <div class="contacts">
                <p>
                    <span class="material-symbols-rounded">mail</span> 
                    <span>{data.email}</span>
                </p>
                <p>
                    <span class="material-symbols-rounded">call</span> 
                    <span>{data.telephone}</span>
                </p>
            </div>
        </div>   
        <p class="description">{data.description}</p> 
        <div class="social">
            {#each data.socials as social}
                {#if social.name === "linkedin"}
                    <a href="{social.url}" target="_blank">
                        <i class="fab fa-{social.name}"></i>
                    </a>
                {:else}
                    <a href="{social.url}" target="_blank">
                        <i class="fab fa-{social.name}-square"></i>
                    </a>
                {/if}
            {/each}
        </div>
    </div>  
</div>

<style>
    .card {
        display: flex;
        flex-direction: row;
        max-width: 1024px;
    }
    .card .text .header {
        display: flex;
        justify-content: space-between;
        align-items: flex-start;
        margin-bottom: 40px;
    }
    .card .text .header .name h1 {
        margin: 0;
        font-size: 24px;
    }
    .card .text .header .name p {
        margin-top: 8px;
        color: var(--text-color-grey);
    }
    .card .text .header p {
        margin: 8px 0;
    }
    .card .text .header .contacts p span {
        display: inline-block;
        vertical-align: middle;
    }
    .card .text p.description {
        color: var(--text-color-grey);
    }
    .card .text .social a {
        position: relative;
        text-decoration: none;
        color: var(--text-color-black);
        font-size: 24px;
        display: inline-block;
        margin: 0 8px 0 0;
    }
    .card img {
        width: 300px;
        height: auto;
        margin-right: 24px;
        border-radius: 12px;
    }
</style>