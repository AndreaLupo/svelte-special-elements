<script>

import CartItem from "./CartItem.svelte";
import FamilyNode from "./FamilyNode.svelte";
import Product from "./Product.svelte";

let y;

$:console.log(y);
let currentTitle='My app';

let familyStructure = [
    {isParent: true, name: 'Chris', children: [
        {isParent: true, name: 'Moe', children: [
            {isParent: false, name: 'Julie'}
        ]}
    ]},
    {isParent: false, name: 'Anna'}
]

let renderedComponent = {cmp: Product, title: 'Test Product', id: 'p1'};
function toggle() {
   if(renderedComponent.cmp ===  Product) {
       renderedComponent = {cmp: CartItem, title: 'Another Product', id: 'p2'};
   } 
   else if(renderedComponent.cmp === CartItem) {
       renderedComponent = {cmp: Product, title: 'Test Product', id: 'p1'};
   }
}

function switchTitle() {
    currentTitle = 'New Title!';
}
</script>

<div>  
    <button on:click={switchTitle}>Switch title</button>

    <button on:click={toggle}>Toggle display</button>


    <svelte:component this={renderedComponent.cmp} title={renderedComponent.title} id={renderedComponent.id}/>

    {#each familyStructure as familyMember}
        <FamilyNode member={familyMember}/>
    {/each}

</div>

<svelte:window on:keydown={(event)=> {console.log(event)}}
        bind:scrollY={y}/>
<svelte:body on:mouseenter={() => {console.log('Mouse Enter')}} />

<!-- everything in the head of the page-->
<svelte:head>
    <title>{currentTitle}</title>

</svelte:head>




<style>
    div {
        height: 3000px;
    }
</style>