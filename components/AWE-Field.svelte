<script>
    export let type = 'text'
    export let value
    export let name
    export let label = name.replace(/_/g, ' ')
    export let placeholder = name.replace(/_/g, ' ')
    export let error = ''
    export let help = ''
    export let required = false
    export let opts = {}

    function inputInit(node, {...data} = {}) {
        //IDEA: have a globals and a named, and check for name
        let options = {...opts, ...data}
        for (let o in options) {
            if (o === 'classes') {
                for (let className of options[o]) {
                    node.classList.add(className)
                }
            } else {
                node[o] = options[o]
            }

        }
    }
</script>

<fieldset class="field">
    <div class='control'>
        {#if label != 'display-none'}
            <label for={name}>{label}</label>
        {/if}
        {#if type === 'text'}
            <input type='text' {name} bind:value {placeholder} {required} use:inputInit />
        {:else if type === 'email'}
            <input type='email' {name} bind:value {placeholder} {required} use:inputInit />
        {:else if type === 'password'}
            <input type='password' {name} bind:value {placeholder} {required} use:inputInit />
        {:else if type === 'hidden'}
            <input type='hidden' {name} bind:value={value} {placeholder} use:inputInit />
        {:else if type === 'select'}
            <slot></slot>
        {:else}
            <input type='text' {name} bind:value={value} {placeholder} {required}>
        {/if}
    </div>
    {#if error}
        <p class='error'>{error}</p>
    {:else if help}
        <p class='help'>{help}</p>
    {/if}
</fieldset>

<style>
    input::placeholder, label {
        text-transform: capitalize;
    }
</style>
