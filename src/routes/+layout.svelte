<script lang="ts">
  import { scroll } from "../stores/scroll";
  import { resizeX, resizeY } from "../stores/resize";
  import { onMount } from "svelte";
  import Header from "./header/header.svelte";
  import "./layout.scss";

  function onScroll() {
    scroll.set(window.scrollY);
  }

  onMount(() => {
    document.body.style.overflowX='hidden';
  })
  

  function OnResize() {
    resizeX.set(window.innerWidth);
    resizeY.set(window.innerHeight);
  }

  onMount(() => {
    OnResize();
  });

  let scrollL: boolean, scrolled: boolean;

  $: if (scrolled && $scroll < 50) {
    scrolled = false;
  } else if(!scrolled && $scroll > 50){
    document.body.style.overflowY = "hidden";
    setTimeout(() => {
    document.body.style.overflowY = "scroll";
    }, 600);
    scrolled = true;
  }
</script>

<svelte:window on:scroll={onScroll} on:resize={OnResize} />
  <Header />
  <slot></slot>
