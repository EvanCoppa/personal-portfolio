<script>
  import { onMount } from "svelte";
  import { base } from "$app/paths";
  import { marked } from "marked";

  export let active;
  export let experienceData;

  let activeSkill = 0;
  let skills = experienceData[active].skills;
  let targetDiv = document.getElementById('markedContainer');

    // This will run whenever targetDiv changes
    $: if (targetDiv) {
        console.log('targetDiv changed!');
        updateDiv();
  }

  function handleClick(i) {
    activeSkill = i;
    updateDiv()  }

 
  function updateDiv() {

    console.log(experienceData[active].skills[activeSkill].isCode);
    // Select the div using its ID

    // Check the condition and set the class
    if (experienceData[active].skills[activeSkill].isCode == true) {
        targetDiv.setAttribute('class', 'w-1/2 bg-[#2d2d2d] rounded-lg m-auto');
    } else {
        targetDiv.setAttribute('class', ''); // or set to some other default class if needed
    }

    // Use marked to parse the text and set it as the innerHTML of the div
    targetDiv.innerHTML = marked(experienceData[active].skills[activeSkill].text);
}

// Sample usage:
// Assume experienceData, active, and activeSkill are already defined.
// updateDiv(experienceData, active, activeSkill);




  // <ExperinceSection index=0 selected={selectedSection === 0} on:click={() => selectSection(0)} class={selectedSection === 0 ? 'red' : 'inherit'} />
  //     <ExperinceSection index=1 selected={selectedSection === 1} on:click={() => selectSection(1)} class={selectedSection === 1 ? 'red' : 'inherit'} />
  //     <ExperinceSection index=2 selected={selectedSection === 2} on:click={() => selectSection(2)} class={selectedSection === 2 ? 'red' : 'inherit'} />
</script>

<div class="experienceSection my-24 flex mx-16">
  <div class="w-1/2 flex flex-col gap-12">
    {#each experienceData[active].skills as skill, i}

      <div
        on:mousedown={() => handleClick(i)}
        class=" transition-all duration-500 rounded-lg w-2/3 px-8 py-4 m-auto {i ===
        activeSkill
          ? 'shadow-2xl'
          : 'hover:shadow-2xl'}"
      >
        <h4 class="text-[rebeccapurple] font-bold">{skill.name}</h4>
        <h5>{skill.description}</h5>
      </div>
    {/each}
 
  </div>

  <!-- {console.log(experienceData[active].skills[activeSkill].isCode)}

  <div  class="{experienceData[active].skills[activeSkill].isCode == true ? 'w-1/2 bg-[#2d2d2d] rounded-lg m-auto' : ''}">
    {marked.parse(experienceData[active].skills[activeSkill].text)}
 </div> -->

    <div id="markedContainer" bind:this={targetDiv}>
    </div>

</div>
