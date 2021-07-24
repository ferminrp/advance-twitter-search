<script>
    export let value = '';
    export let placeholder;
</script>

<p><slot><!-- optional fallback --></slot></p>
<input type="text" bind:value {placeholder}>

<style>
    input {
        margin-bottom: 1rem;
        width: 100%;
        border: 0px;
        border-bottom: 2px solid #1b91db;
        background-color: #f0f7fa;
    }
    p {
        font-weight: 600;
    }
</style>