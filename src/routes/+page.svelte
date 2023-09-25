<script>
    import ExperinceSection from "../lib/componets/experinceSection.svelte";
    import experienceData from "$lib/data/experience.json";
    var experiences = experienceData.experiences;
    var active = 0;
</script>

<svelte:head>
    <title>Home</title>
</svelte:head>



<div class=" relitive " style="font-family: 'IBM Plex Mono', monospace; ">
    <div class="bg-zinc-100 pb-48 pt-16 px-16">
        <h1 class="text-7xl font-bold text-[rebeccapurple] leading-[5rem]">
            I'M <span class="font-light">Evan Coppa</span>, <br /> A STUDENT WEB
            DEVELOPER
        </h1>
        <h4 class="italic text-3xl">Check out my experience:</h4>
    </div>

    <div class="bg-white p-8   translate-y-[-5rem] w-[75vw] max-w-[1000px] m-auto rounded-lg drop-shadow-lg flex gap-4 justify-around">
        {#each experiences as experience, i}
            <h5 on:click={() => active = i} class="hover:scale-110 tranistion-all duration-500 {active === i ? 'underline' : ''}" >{experience.title}</h5>
        {/each}
    </div>

    <div class="">
        <ExperinceSection  active="{active}" />
    </div>
</div>
