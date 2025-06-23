<script lang="ts">
    import { resizeX, resizeY } from "../../stores/resize";
    import {aba} from "../../stores/aba";
    import HeaderPC from "./devices/pc.svelte";
    import { lang, t } from "../../stores/lang";

    let razão: number;
    $: razão = $resizeX / $resizeY;

    let TXTHeader: any;
    $: {
        $lang;
        TXTHeader = {
            header: {
                txt: t("header.txt")
            },
            nav: {
                home : t('nav.home'),
                sobre: t("nav.sobre"),
                documentos: t("nav.documentos"),
                playground: t("nav.playground"),
            },
        };
    }

</script>

{#if razão > 0.63}
    <HeaderPC tradução={TXTHeader} />

    <!--{:else}-->
{/if}
