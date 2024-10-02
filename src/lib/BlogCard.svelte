<script>
// @ts-nocheck
export let blogData
import { Circle } from 'svelte-loading-spinners';
</script>

<div class="card">
    <h4>Blog</h4>
    {#if Object.keys(blogData).length === 0}
    <div class="spinner"><Circle size="60" color="#4f4f4f" unit="px" /></div>
    {:else} 
    <div class="header">
        <img src="{blogData.cover_image}" alt="" />
        <h3>{blogData.title}</h3>
    </div>
    <p>{blogData.description}</p>
    <a href="{blogData.url}" alt="" target="_blank">dev.to</a>
    {/if}
</div>

<style>
    .card {
        height: 520px;
    }
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
    .spinner {
        height: 100%;
        width: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
    }
</style>
