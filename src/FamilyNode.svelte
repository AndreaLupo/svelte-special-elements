<script context="module">
    console.log('Runs once!');

    let deactivateNode;
</script>
<script>
    console.log('Runs multiple times');
    export let member;

    let isActive;

    function activate() {
        if(deactivateNode) {
          deactivateNode();  
        }
        isActive = true;
        /* add a pointer in the module to the function of the current
            component */
            deactivateNode = deactivate;
    }

    function deactivate() {
        isActive = false;
        
    }
</script>

<div on:click={activate} class:active={isActive}>
    <h1>{member.name}</h1>
    {#if member.isParent}
        {#each member.children as child}
            <svelte:self member={child}/>
        {/each}
    {/if}        
</div>

<style>
    div {
        margin-left: 2rem;
    }

    .active {
        color: red;
    }
</style>