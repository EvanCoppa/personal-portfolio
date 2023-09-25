<script>
  import { onMount } from "svelte";
  import { page } from "$app/stores";
  import { navigating } from "$app/stores";
  $: if ($navigating) {
    messageColor = $page.url.pathname == "/" ? "bg-zinc-100" : "";
    console.log("hello");
  }
  // Inside a Svelte component

  var pageTitle = "";
  var message = "";
  var messageColor = "";

  messageColor = $page.url.pathname == "/" ? "bg-zinc-100" : "";

  onMount(() => {
    pageTitle = document.title;
    message = "Welcome 👋";
  });
</script>

<nav class="flex max-w-screen justify-between {messageColor}  px-12 py-4">
  <div
    class="flex font-['Open_Sans'] text-3xl"
    style="font-family: 'IBM Plex Mono', monospace; "
  >
    <h3 class="m-auto">{pageTitle}</h3>
    <span class=" text-5xl font-thin"> | </span>
    <h4
      class="text-lg m-auto pt-1 font-thin"
      style="font-family: 'IBM Plex Sans';"
    >
      {message}
    </h4>
  </div>
  <div class="flex gap-8 my-auto [&>*]:font-['Open_Sans']">
    <a class="" href="/">Home</a>
    <a href="/about">About</a>
    <a href="/blog">Blog</a>
    <a href="/about" class="text-[rebeccapurple]">Subscribe</a>
  </div>
</nav>
