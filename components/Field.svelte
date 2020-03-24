<script>
    export let type = 'text'
    export let value
    export let name
    export let label = name.replace('_', ' ')
    export let placeholder = name
    export let errors = []
    export let help = ''
    export let required = false
    export let classes = ""
</script>

<fieldset class="field {classes}">
    <div class='control'>
        {#if type === 'text'}
            <input type='text' {name} bind:value {placeholder} {required}>
        {:else if type === 'email'}
            <input type='email' {name} bind:value {placeholder} {required}>
        {:else if type === 'password'}
            <input type='password' {name} bind:value {placeholder} {required}>
        {:else if type === 'hidden'}
            <input type='hidden' {name} bind:value={value} {placeholder}>
        {:else}
        <input type='text' {name} bind:value={value} {placeholder} {required}>
        {/if}
        {#if label != 'display-none'}
            <label for={name}>{label}</label>
        {/if}
    </div>
    {#if errors.length}
        <p class='error'>{errors[0]}</p>
    {:else if help}
        <p class='help'>{help}</p>
    {/if}
</fieldset>

<style>
    input::placeholder, label {
        text-transform: capitalize;
    }
</style>
