<script>
    import Navbar from "$lib/components/navbar.svelte";
    let video = "/images/asosi.mp4"
</script>
<main>
    <Navbar />
    <video muted autoplay loop class="brightness-70"  src={video}></video>
</main>

