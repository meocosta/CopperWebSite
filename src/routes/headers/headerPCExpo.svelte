<script lang="ts">
    import { Info, CircleX } from "lucide-svelte";
    import { aba } from "../../stores/aba";
    import { scroll } from "../../stores/scroll";
    import { lang } from "../../stores/lang";
    import "./headerPCExpo.scss";
    export let tradução: any;

    let nav: boolean = false;

    $: scrolled = $scroll > 50;
</script>

<header>
    <p>{tradução.header.txt}</p>
    <div id="titleHeader">
        <h1 id="h1">Copper</h1>
        <h1 id="sombrah1">Copper</h1>
    </div>
</header>

