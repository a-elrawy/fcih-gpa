<script>
    import Card from "$lib/components/Card.svelte";
    export let cards;
</script>
<div class="flex justify-center flex-wrap m-5">
    {#each cards as card}
        <Card card="{card}" />
    {/each}
</div>