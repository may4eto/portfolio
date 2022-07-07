<script>
    export let data
</script>
<main>
    <div class="card">
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
        </div>  
    </div>
</main>
<style>
    .card {
        padding: 24px;
        display: flex;
        flex-direction: row;
        max-width: 1024px;
        background-color: #fff;
        border-radius: 12px;
        -webkit-box-shadow: 0px 4px 8px 0px rgba(0,0,0,0.25); 
        box-shadow: 0px 4px 8px 0px rgba(0,0,0,0.25);
        box-sizing: border-box;
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
    .card img {
        width: 300px;
        height: auto;
        margin-right: 24px;
        border-radius: 12px;
    }
</style>