<script>
  import FirestoreParser from "firestore-parser";

  let items = [];

  // API URL
  const baseUrl = "https://firestore.googleapis.com/v1/";
  const articlesUrl =
    baseUrl +
    "projects/first-firestore-8b4b3/databases/(default)/documents/artikkelregister";

  const getArticles = () => {
    fetch(articlesUrl)
      // turns the data we are fetching into json
      .then(response => response.json())
      // sends json trough the firestore parser making it easier to read
      .then(json => FirestoreParser(json))
      .then(parsed => (items = parsed.documents))
      // picks up errors and sends it to the console log
      .catch(error => console.log(error));
  };

  getArticles();
</script>

<style>
  .spinner {
    margin-top: 24;
  }

  .main {
    background-color: #1e1c22;
  }
  .article {
    margin: 16 8 16 16;
    background-color: #292b33;
    flex-direction: column;
  }
  .article-tekst {
    padding: 16 8 16 8;
  }
  .article > image {
    height: 200;
    margin-bottom: 16;
  }
  .h2 {
    color: #ebd5bb;
  }
  .body {
    color: #ebd5bb;
  }
</style>

<page>
  <actionBar title="Bjørneposten" />
  <scrollView class="main">
    <stackLayout>
      {#each items as item}
        <flexboxLayout class="article">
          <image
            src={item.fields.url}
            alt="article image"
            stretch="aspectFit" />
          <stackLayout class="article-tekst">
            <label class="h2" text={item.fields.tittel} />
            <label class="body" text={item.fields.tid} />
            <label class="body" text={item.fields.ingress} />
          </stackLayout>
        </flexboxLayout>
      {:else}
        <activityIndicator busy={true} class="spinner" />
      {/each}
    </stackLayout>
  </scrollView>
</page>
