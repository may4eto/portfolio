<script>
// @ts-nocheck
export let blogData 
</script>

<div class="card">
    <h4>Blog</h4>
    <div class="header">
        <img src="{blogData.cover_image}" alt="" />
        <h3>{blogData.title}</h3>
    </div>
    <p>{blogData.description}</p>
    <a href="{blogData.url}" alt="" target="_blank">dev.to</a>
</div>

<style>
    .card h3 {
        font-size: 24px;
        margin-top: 8px;
        line-height: 1.2;
    }
    .card h4 {
        font-size: 16px;
        color: var(--light-grey);
        margin-top: 0;
    }
    .card p, .card a {
        font-size: 16px;
        color: var(--text-color-grey);
    }
    .card .header img {
        width: 100%;
        border-radius: 12px;
    }
</style>
