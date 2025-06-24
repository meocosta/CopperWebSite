<script lang="ts">
    import { lang, t } from "../../stores/lang";
    import HeaderPC from "./headerPCExpo.svelte";
    import { resizeX, resizeY } from "../../stores/resize";
    import { experience } from "../../stores/experience";
    import { aba } from '../../stores/aba';
    import { Info, CircleX } from "lucide-svelte";

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

{#if razão > 0.63 && $experience}
    <HeaderPC tradução={tradução} />
{/if}