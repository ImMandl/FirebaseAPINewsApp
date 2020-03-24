<script>
  import FirestoreParser from "firestore-parser";

  let items = [];

  const baseUrl = "https://firestore.googleapis.come/v1/";
  const articlesUrl =
    baseUrl +
    "projects/first-firestore-8b4b3/databases/(default)/documents/artikkelregister";

  const getArticles = () => {
    fetch(articlesUrl)
      // turns the data we are fetching into json
      .then(response => response.json())
      // sends json trough the firestore parser making it easier to read
      .then(json => FirestoreParser(json))
      .then(parsed => {
        items = parsed.documents;
        console.log(items);
      })
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
    background-color: #fff;
  }
  .article {
    margin: 8 8 0 8;
    background-color: brown;
    flex-direction: column;
  }
  .article > image {
    height: 200;
    margin-bottom: 16;
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
          <stackLayout>
            <label class="h2" text={item.fields.tittel} />
            <label class="body" text={item.fields.tid} />
          </stackLayout>
        </flexboxLayout>
      {:else}
        <activityIndicator busy={true} class="spinner" />
      {/each}
    </stackLayout>
  </scrollView>
</page>
