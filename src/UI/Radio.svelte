<script>
    export let options = [];
    export let group = options[0];

</script>

<div>
{#each options as option}
    <label>
        <input type="radio" bind:group name="scoops" value={option} />
        {option}
    </label>
{/each}
</div>

<style>
    div {
        margin-top: 0.7rem;
        margin-bottom: 2rem;
    }
</style>
