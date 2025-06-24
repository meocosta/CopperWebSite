<script lang="ts">
    import { scroll } from "../stores/scroll";
    import { lang, t } from "../stores/lang";
    import { resizeX, resizeY } from "../stores/resize";
    import { onMount } from "svelte";
    import "./+layout.scss";
    import { Info, CircleX } from "lucide-svelte";
    import Header from "./headers/Header.svelte";
    import Nav from "./headers/Nav.svelte";
    import {experience} from "../stores/experience";

    onMount(() => {
        OnResize();
        //pra não ter chance de ter scroll horizontal
        document.body.style.overflowX = "hidden";
    });

    function OnResize() {
        resizeX.set(window.innerWidth);
        resizeY.set(window.innerHeight);
    }

    function onScroll() {
        scroll.set(window.scrollY);
    }

    function changeLang(language: string) {
        lang.set(language);
    }

    let traduction: any;
    $: {
        $lang;
        traduction = {
            alert: {
                titulo: t("alert.titulo"),
                txt: t("alert.txt"),
            },
        };
    }
</script>

<svelte:window on:scroll={onScroll} on:resize={OnResize} />

<section id="CopperWebSite" class:expo={$experience}>
    <section id="conteudoCopperWebSite">
        <Header />
        <div id="headerSpace" style="height:{$experience ? 100 : 10}vh"></div>
        <slot />
    </section>
    
    <Nav />
    <div id="navSpace"></div>
</section>
