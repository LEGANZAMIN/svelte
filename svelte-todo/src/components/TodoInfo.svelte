<script>
    export let todoCount;
    export let handleChangeViewMode;
    export let viewMode;

    import Constant from "../constant";
</script>

<style>
    .selected {
        border-bottom: 5px solid #005eff;
    }
</style>

<div class="info">
    <div class="wrap">
        <span> COUNT: {todoCount}</span>
        <div>
            <button class="btn" class:selected={viewMode === Constant.ALL} on:click={() => handleChangeViewMode(Constant.ALL)}>ALL</button>
            <button class="btn" class:selected={viewMode === Constant.ACTIVE} on:click={() => handleChangeViewMode(Constant.ACTIVE)}>ACTIVE</button>
            <button class="btn" class:selected={viewMode === Constant.DONE} on:click={() => handleChangeViewMode(Constant.DONE)}>DONE</button>
        </div>
    </div>
</div>
