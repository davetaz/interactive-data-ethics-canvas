<script lang="ts">
    import { canvasState } from '../../store';
    import { getLocalization } from '../../i18n';
    import Textarea from '../form/Textarea.svelte';

    export let ref: number;
  
    const { t } = getLocalization();
    const id = canvasState.getBlobId(ref);
</script>

{#each $t('areas:' + id + '.questions', { returnObjects: true }) as l, i }
    <Textarea question={ l } bind:content={ $canvasState.blobs[ref].content[i] } />
{/each}