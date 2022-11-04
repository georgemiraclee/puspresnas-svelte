<script>
    import { fade } from 'svelte/transition';
</script>

<div class="overlay" transition:fade="{{delay: 0, duration: 300}}">
    <p>Loading...</p>
</div>