<script>
  import { page } from "$app/stores";
  import { marked } from "marked";
  import { onMount } from "svelte";
 
  import "./style.css";

  const blogId = $page.params.blogId;
  console.log($page.params);
  var article;
 
  onMount(async () => {
    const response = await fetch(`/src/lib/articles/${blogId}.md`);
     article = marked.parse(await response.text());
    document.title = blogId;
    setTimeout(() => {
      Prism.highlightAll();
      createCopyButtons();
    }, 0);
  });

  function createCopyButtons() {
    const copyButtonLabel = "Copy";
     // use a class selector if available
    let blocks = document.querySelectorAll("pre");

    blocks.forEach((block) => {
      // only add button if browser supports Clipboard API
      if (navigator.clipboard) {
        let button = document.createElement("button");

        button.innerText = copyButtonLabel;
        block.appendChild(button);

        button.addEventListener("click", async () => {
          await copyCode(block, button);
        });
      }
    });

    async function copyCode(block, button) {
      let code = block.querySelector("code");
      let text = code.innerText;

      await navigator.clipboard.writeText(text);

      // visual feedback that task is completed
      button.innerText = "Code Copied";

      setTimeout(() => {
        button.innerText = copyButtonLabel;
      }, 700);
    }
  }

  //   var article = new File(fileParts, fileName, [options]);
</script>

<div class="mx-auto my-12 max-w-[80vw] content" >
  {@html article}
 </div>
