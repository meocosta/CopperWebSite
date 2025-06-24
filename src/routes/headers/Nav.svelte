<script lang="ts">
    import { lang, t } from "../../stores/lang";
    import { resizeX, resizeY } from "../../stores/resize";
    import { experience } from "../../stores/experience";
    import { aba } from "../../stores/aba";
    import { Info, CircleX } from "lucide-svelte";
    import "./Nav.scss";

    export let checked = true;
    export let onChange = () => {
        experience.set(checked);
    };

    let razão: number;
    $: razão = $resizeX / $resizeY;

    let tradução: any;
    $: {
        $lang;
        tradução = {
            header: {
                txt: t("header.txt"),
            },
            nav: {
                home: t("nav.home"),
                sobre: t("nav.sobre"),
                documentos: t("nav.documentos"),
                playground: t("nav.playground"),
            },
        };
    }

    let nav: boolean = false;
    let info: boolean = false;

    function changeAba(tab: string) {
        aba.set(tab);
    }

    function changeLang(language: string) {
        lang.set(language);
    }
</script>

<nav style="right: {$experience ? 0 : 2.5}vw">
    <div id="Navegation">
        <button on:click={() => (nav = !nav)}>
            <CircleX
                class="icons"
                size={50}
                style="transform: rotate({nav ? 0 : 45}deg);"
            />
        </button>
    </div>

    {#if razão > 0.63 && $experience}
        <div id="scrollBar">
            <div></div>
        </div>
    {/if}

    <div id="language">
        <button
            on:click={() => changeLang("pt_br")}
            class={$lang == "pt_br" ? "ativo" : "inativo"}>PT</button
        >
        <p>|</p>
        <button
            on:click={() => changeLang("en_us")}
            class={$lang == "en_us" ? "ativo" : "inativo"}>EN</button
        >
    </div>

    <div id="expoMode">
        <p>expo mode</p>
        <label class="switch">
            <input type="checkbox" bind:checked on:change={onChange} />
            <span class="slider"></span>
        </label>
    </div>

    <div id="navOpen" style="margin-left: {nav ? '0' : '60'}vw">
        <a
            class:overline={$aba == "home"}
            class:aparecer={nav}
            on:click={() => changeAba("home")}
            href="/home"
        >
            {tradução.nav.home}
        </a>
        <a
            class:overline={$aba == "sobre"}
            class:aparecer={nav}
            on:click={(e) => {
                changeAba("sobre");
            }}
            href="/sobre">{tradução.nav.sobre}</a
        >
        <a
            class:overline={$aba == "docs"}
            class:aparecer={nav}
            on:click={(e) => {
                changeAba("docs");
            }}
            href="/documentos">{tradução.nav.documentos}</a
        >
        <a
            class:overline={$aba == "playground"}
            class:aparecer={nav}
            on:click={(e) => {
                changeAba("playground");
            }}
            href="/playground">{tradução.nav.playground}</a
        >
    </div>
</nav>
