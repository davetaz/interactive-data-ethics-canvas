<script lang="ts">
    import { canvasState } from '../../store';
    import { getLocalization } from '../../i18n';
    import Textarea from '../form/Textarea.svelte';
    import DynamicList from '../form/DynamicList.svelte';
    import BooleanAndTextarea from '../form/BooleanAndTextarea.svelte';
    import DataRight from '../form/DataRight.svelte';

    export let ref: number;

    let sources = [];
    const sourcesBlob = $canvasState.blobs.find(element => element.id == "sources");
    if (sourcesBlob && sourcesBlob.content && sourcesBlob.content.length > 0) {
        sources = sourcesBlob.content;
    }
  
    const { t } = getLocalization();
    const id = canvasState.getBlobId(ref);
</script>


{#if sources.length == 0}
    <p>Please complete the Data Sources section before filling in the rights around your data sources.</p>
{:else}
    {#each sources as l, i}
        {#if l.title}
            <DataRight title={ l.title } sourceIndex={i} bind:content={ $canvasState.blobs[ref].content[i] } />
        {/if}
    {/each}
{/if}
