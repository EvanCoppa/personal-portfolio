<script>
    import { onMount } from "svelte";
     export let active;
    let activeSkill = 0;
    import experienceData from "$lib/data/experience.json";
     var experienceSkills = experienceData.experiences[active].skills;

    // Assuming 'experiences' is the given array
    onMount(() => {
        console.log();
    });

    function handleClick(i){
        activeSkill = i;
        console.log(activeSkill);
    };

    function test() {
        alert("test");
    }
    // <ExperinceSection index=0 selected={selectedSection === 0} on:click={() => selectSection(0)} class={selectedSection === 0 ? 'red' : 'inherit'} />
    //     <ExperinceSection index=1 selected={selectedSection === 1} on:click={() => selectSection(1)} class={selectedSection === 1 ? 'red' : 'inherit'} />
    //     <ExperinceSection index=2 selected={selectedSection === 2} on:click={() => selectSection(2)} class={selectedSection === 2 ? 'red' : 'inherit'} />
</script>

<div class="experienceSection my-24 flex mx-16">
    <div class="w-1/2 flex flex-col gap-12">
        {#each experienceSkills as skill, i}
        <div on:mousedown={() => handleClick(i)} class=" transition-all duration-500 rounded-lg w-2/3 px-8 py-4 m-auto {i === activeSkill ? 'shadow-2xl' : 'hover:shadow-2xl'}">
            <h4 class="text-[rebeccapurple] font-bold">{skill.name}</h4>
            <h5>{skill.description}</h5>
        </div>
        
        {/each}
    </div>

    <div class="w-1/2 bg-[#2d2d2d] rounded-lg m-auto">
        <pre class="language-python" tabindex="0"><code class="language-python"><span class="token decorator annotation punctuation">@app<span class="token punctuation">.</span>route</span><span class="token punctuation">(</span><span class="token string">'/&lt;path:filename&gt;'</span><span class="token punctuation">)</span> 
            <span class="token keyword">def</span> <span class="token function">markdown_to_html</span><span class="token punctuation">(</span>filename<span class="token punctuation">)</span><span class="token punctuation">:</span>    
                md_file <span class="token operator">=</span> os<span class="token punctuation">.</span>path<span class="token punctuation">.</span>join<span class="token punctuation">(</span><span class="token string">'path/to/markdown/files'</span><span class="token punctuation">,</span> filename <span class="token operator">+</span> <span class="token string">'.md'</span><span class="token punctuation">)</span>     
                    <span class="token keyword">if</span> <span class="token keyword">not</span> os<span class="token punctuation">.</span>path<span class="token punctuation">.</span>exists<span class="token punctuation">(</span>md_file<span class="token punctuation">)</span><span class="token punctuation">:</span>         
                        <span class="token keyword">return</span> <span class="token string">'File not found'</span><span class="token punctuation">,</span> <span class="token number">404</span>      
                    <span class="token keyword">with</span> <span class="token builtin">open</span><span class="token punctuation">(</span>md_file<span class="token punctuation">,</span> <span class="token string">'r'</span><span class="token punctuation">)</span> <span class="token keyword">as</span> <span class="token builtin">file</span><span class="token punctuation">:</span>        
                        markdown_text <span class="token operator">=</span> <span class="token builtin">file</span><span class="token punctuation">.</span>read<span class="token punctuation">(</span><span class="token punctuation">)</span>         
                        html_content <span class="token operator">=</span> markdown<span class="token punctuation">.</span>markdown<span class="token punctuation">(</span>markdown_text<span class="token punctuation">)</span>      
            
                    <span class="token keyword">return</span> render_template<span class="token punctuation">(</span><span class="token string">'page.html'</span><span class="token punctuation">,</span> content<span class="token operator">=</span>html_content<span class="token punctuation">)</span>
            </code><button>Copy</button></pre>

     </div>
</div>
