<script lang="ts">
  import { page } from '$app/stores';

  import type { PageData } from './$types';

  export let data: PageData;

  $: supabase = data.supabase;

  let loadedData = [];
  const loadData = async () => {
    const { data } = await supabase.from('todos').select('*').limit(20);
    loadedData = data;
  };

  $: if ($page.data.session) {
    loadData();
  }
</script>

{#if $page.data.session}
  <p>client-side data fetching with RLS</p>
  <pre>{JSON.stringify(loadedData, null, 2)}</pre>
{/if}
