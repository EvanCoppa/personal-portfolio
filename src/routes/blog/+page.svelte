<script>
  import { onMount } from "svelte";

    var articles;

onMount(async () => {
   // for each file in `/src/lib/articles/` create link with the title of the file
    const response = await fetch(`/src/lib/articles/`);
    const files = await response.json();
    const articles = document.getElementById("articles");
    files.forEach((file) => {
      const link = document.createElement("a");
      link.href = `/blog/${file}`;
      link.innerText = file;
      articles.appendChild(link);
    });
});
    
         </script>

        <h1>Welcome to the blog</h1>

        <div id="articles"></div>