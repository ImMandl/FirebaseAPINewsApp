<script>
  import Article from "../modals/Article.svelte";
  import { showModal } from "svelte-native";
  import { registerNativeViewElement } from "svelte-native/dom";

  export let articles;

  // gives box shadow
  registerNativeViewElement(
    "cardView",
    () => require("@nstudio/nativescript-cardview").CardView
  );

  // shows articles when a news tiled is prressed
  const showArticle = async article => {
    await showModal({
      page: Article,
      props: {
        article: article
      }
    });
  };
</script>

<style>
  .main {
    background-color: #eee;
  }
  .article {
    margin: 0 8 0 8;
    background-color: #fff;
    flex-direction: column;
  }
  .article-tekst {
    padding: 16 8 16 8;
  }
  .article > image {
    margin-top: 0;
    margin-bottom: 0;
    width: 100%;
    height: 210;
    object-fit: cover;
  }
  .h2 {
    color: #292b33;
  }
  .body {
    color: #292b33;
  }
</style>

<scrollView>
  <stackLayout class="main">
    {#each articles as article}
      <cardView margin="8" elevation="40">
        <flexboxLayout class="article" on:tap={() => showArticle(article)}>
          <image
            src={article.fields.url}
            alt="article image"
            stretch="aspectFit" />
          <stackLayout class="article-tekst">
            <label class="h2" text={article.fields.tittel} />
            <label class="body" text={article.fields.tid} />
            <label class="body" text={article.fields.ingress} />
          </stackLayout>
        </flexboxLayout>
      </cardView>
    {:else}
      <activityIndicator busy={true} class="spinner" />
    {/each}
  </stackLayout>
</scrollView>
