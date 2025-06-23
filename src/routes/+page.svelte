<script lang="ts">
    import "./page.scss";
    import { scroll } from "./../stores/scroll";

    $: scrolled = $scroll > 50;
</script>

<section id="IntroHomeContainer">
    <div id="fundo" class:scrolled={scrolled}></div>
    <div id="StartNow" class:scrolled={scrolled}>
        <h2>Copper: a nova linguagem baseada em Rust</h2>
        <button>Comece agora!</button>
    </div>
</section>
