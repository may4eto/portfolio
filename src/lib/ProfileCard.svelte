<script>
    export let data
</script>

<header class="card profile">
    <figure>
        <img src="images/profile-image.jpg" alt="Maya Mircheva, Front-end developer" />
    </figure>
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
</header>

<style>
    .card {
        display: flex;
        flex-direction: row;
        max-width: 1024px;
    }
    .card figure {
        margin: 0;
    }
    .card .text .header {
        display: flex;
        justify-content: space-between;
        align-items: flex-start;
        margin-bottom: 32px;
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
        filter: grayscale(100%) blur(0.25px) contrast(33%) brightness(1.025);
        mix-blend-mode: hard-light;
    }
    @media (max-width: 1024px) {
        .card .text .social {
            margin-top: 40px;
        }
    }
    @media (max-width: 986px) {
        .card .text {
            font-size: 16px;
        }
        .card .text .header {
            margin-bottom: 24px;
        }
    }
    @media (max-width: 972px) {
        .card .text .social {
            margin-top: 24px;
        }
    }
    @media(max-width: 950px) {
        .card .text .header {
            flex-direction: column;
            justify-content: flex-start;
            margin-bottom: 24px;
        }
        .card figure {
            display: flex;
            align-items: center;
            justify-content: center;
        }
    }
    @media(max-width: 835px) {
        .card {
            flex-direction: column;
        }
        .card figure {
            margin-bottom: 24px;
        }
        .card figure img {
            margin-right: 0;
            width: 100%;
        }
        .card .text .social a {
            font-size: 40px;
            margin: 0 16px 0 0;
        }
    }
</style>