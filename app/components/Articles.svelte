<script>
  import Article from "../modals/Article.svelte";
  import { showModal } from "svelte-native";
  export let articles;

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
    margin: 16 8 16 16;
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
    height: 220;
    object-fit: cover;
  }
  .h2 {
    color: #292b33;
  }
  .body {
    color: #292b33;
  }
</style>

<scrollView class="main">
  <stackLayout>
    {#each articles as article}
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
    {:else}
      <activityIndicator busy={true} class="spinner" />
    {/each}
  </stackLayout>
</scrollView>
