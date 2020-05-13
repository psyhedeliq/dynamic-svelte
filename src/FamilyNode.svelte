<script context="module">
  // the below code runs only once per module/file unlike in the other script tag that runs once per instance
  // this is useful if you want to share data across all components of the same type
  console.log("Runs once!");

  let deactivateNode;
</script>

<script>
  // this script tag runs onace per instance which is the defaul for svelte
  export let member;

  let isActive;

  console.log("Runs multiple times!");

  const deactivate = () => {
    isActive = false;
  };

  const activate = () => {
    if (deactivateNode) {
      deactivateNode();
    }
    isActive = true;
    deactivateNode = deactivate;
  };
</script>

<style>
  div {
    margin-left: 2rem;
  }

  .active {
    color: red;
  }
</style>

<div on:click={activate} class:active={isActive}>
  <h1>{member.name}</h1>
  {#if member.isParent}
    {#each member.children as child}
      <svelte:self member={child} />
    {/each}
  {/if}
</div>
