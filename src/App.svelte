<script>
import CartItem from "./CartItem.svelte";
import Product from "./Product.svelte";

let renderedComponent = {cmp: Product, title: 'Test Product', id: 'p1'};
function toggle() {
   if(renderedComponent.cmp ===  Product) {
       renderedComponent = {cmp: CartItem, title: 'Another Product', id: 'p2'};
   } 
   else if(renderedComponent.cmp === CartItem) {
       renderedComponent = {cmp: Product, title: 'Test Product', id: 'p1'};
   }
}
</script>

<button on:click={toggle}>Toggle display</button>


<svelte:component this={renderedComponent.cmp} title={renderedComponent.title} id={renderedComponent.id}/>
    