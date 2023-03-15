<script lang="ts">
  import { goto } from '$app/navigation';

  import type { PageData } from './$types';

  export let data: PageData;

  $: supabase = data.supabase;

  let email = '';
  let isNewRegistration = false;

  const signUp = async () => {
    let { data, error } = await supabase.auth.signUp({
      email: email,
      password: 'GXbwRDToUIQVqLfxLURy',
    });
    goto('/');
  };

  const signIn = async () => {
    let { data, error } = await supabase.auth.signInWithPassword({
      email: email,
      password: 'GXbwRDToUIQVqLfxLURy',
    });
    goto('/');
  };
</script>

<label for="">
  Email:
  <input type="email" bind:value={email} placeholder="email@email.com">
</label>
<br>
{#if isNewRegistration}
  <button on:click={signUp}>SignUp</button>
  <p on:click={() => (isNewRegistration = false)} class="switch">
    Already have an account?
  </p>
{:else}
  <button on:click={signIn}>SignIn</button>
  <p on:click={() => (isNewRegistration = true)} class="switch">
    Create a new account?
  </p>
{/if}
