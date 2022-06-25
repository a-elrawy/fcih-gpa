<script >
    export let card;
</script>
<div class="card max-w-2xl m-2 ">
    <div class="card-body bg-base-200 py-20">
        <h5 class="text-3xl font-bold text-center ">{card.title}</h5>
        <p class="card-text ">{card.description}</p>
        <a href="{card.id}" class="btn btn-primary">Go somewhere</a>
    </div>
</div>