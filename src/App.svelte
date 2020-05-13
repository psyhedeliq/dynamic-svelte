<script>
  import Product from "./Product.svelte";
  import CartItem from "./CartItem.svelte";
  import FamilyNode from "./FamilyNode.svelte";

  let y;

  $: console.log(y);

  let currentTitle = "My App";

  let familyStructure = [
    {
      isParent: true,
      name: "Chris",
      children: [
        {
          isParent: true,
          name: "John",
          children: [{ isParent: false, name: "Julie" }]
        }
      ]
    },
    { isParent: false, name: "Anna" }
  ];

  let renderedComponent = { cmp: Product, title: "Test Product", id: "p1" };

  const toggle = () => {
    if (renderedComponent.cmp === Product) {
      renderedComponent = { cmp: CartItem, title: "Another Product", id: "p2" };
    } else {
      renderedComponent = { cmp: Product, title: "Test Product", id: "p1" };
    }
  };

  const switchTitle = () => {
    currentTitle = "Amazing Coding Machine";
  };
</script>

<style>
  /* we add this to test the scrollY below */
  div {
    height: 3000px;
  }
</style>

<svelte:window bind:scrollY={y} />

<!-- the svelte:body is for interacting with events on the body document -->
<svelte:body on:mouseenter />

<!-- in the svelte:head we can add any elements that would normally be in the head seaction of the ccomponent -->
<svelte:head>
  <title>{currentTitle}</title>
</svelte:head>

<button on:click={switchTitle}>Switch Title</button>

<div>
  <button on:click={toggle}>Toggle Display</button>

  <svelte:component
    this={renderedComponent.cmp}
    title={renderedComponent.title}
    id={renderedComponent.id} />

  {#each familyStructure as familyMember}
    <FamilyNode member={familyMember} />
  {/each}
</div>
