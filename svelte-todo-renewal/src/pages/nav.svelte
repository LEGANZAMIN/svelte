<script>
    import { url, isActive } from "@sveltech/routify";

    let id = "test";
</script>

<style>
    .located {
        border-bottom: 2px solid #005eff;
    }
</style>

<nav class="menu-box">
    <a href={$url('/index')} class:located={$isActive('./index')} class="btn">Home</a>
    <a href={$url('/about/:id', { id: id })} class:located={$isActive('./about')} class="btn">About</a>
    <a href={$url('/todo')} class:located={$isActive('./todo')} class="btn">Todos</a>
</nav>
