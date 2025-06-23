<script lang="ts">
    import { lang } from "../../../stores/lang";
    import { scroll } from "../../../stores/scroll";
    import { aba } from "../../../stores/aba";
    import "./pc.scss";

    export let tradução: any;

    let header: HTMLElement;
    let shrink = false;
    let preshrink = shrink;
    let txt: HTMLElement;

    const animaçãoTxt = (entrar: boolean) => {
        if (txt) {
            if (entrar) {
                txt.classList = "entrada";
                txt.style.opacity = "0";
                setTimeout(() => {
                    shrink = true;
                    setTimeout(() => {
                        txt.style.display = "none";
                    }, 500);
                }, 150);
            } else {
                txt.classList = "saida";
                txt.style.display = "block";
                shrink = false;
                setTimeout(() => {
                    txt.style.opacity = "1";
                }, 500);
            }
        }
    };
    $: preshrink = $scroll > 50;
    $: animaçãoTxt(preshrink);

    function changeAba(NewAba: string) {
        aba.set(NewAba);
    }
</script>

<header id="HeaderPC" bind:this={header} class:shrink>
    <div id="titleHeaderPC">
        <p bind:this={txt}>{tradução.header.txt}</p>
        <div id="titleContainer">
            <h1 id="title">Copper</h1>
            <h1 id="titleShadow">Copper</h1>
        </div>
    </div>
    <nav>
        <a
            on:click={(e) => {
                changeAba("home");
            }}
            href="/home">{tradução.nav.home}</a
        >
        <a
            on:click={(e) => {
                changeAba("sobre");
            }}
            href="/sobre">{tradução.nav.sobre}</a
        >
        <a
            on:click={(e) => {
                changeAba("docs");
            }}
            href="/documentos">{tradução.nav.documentos}</a
        >
        <a
            on:click={(e) => {
                changeAba("playground");
            }}
            href="/playground">{tradução.nav.playground}</a
        >
        <select bind:value={$lang}>
            <option value="en_us">EN</option>
            <option value="pt_br">PT</option>
        </select>
    </nav>
</header>
