<script>
  import { showModal } from "svelte-native";
  import FirestoreParser from "firestore-parser";
  import Articles from "./components/Articles.svelte";

  let articles = [];
  let news = [];
  let sport = [];
  let culture = [];

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
      .then(parsed => {
        news = parsed.documents.filter(art => art.fields.kategori == "nyhet");
        sport = parsed.documents.filter(art => art.fields.kategori == "sport");
        culture = parsed.documents.filter(
          art => art.fields.kategori == "kultur"
        );
      })
      // picks up errors and sends it to the console log
      .catch(error => console.log(error));
  };

  getArticles();

  let selectedTab = 0;
</script>

<page>
  <actionBar title="Bjørneposten" />
  <tabs bind:selectedIndex={selectedTab}>

    <!-- The bottom tab UI is created via TabStrip (the containier) and TabStripItem (for each tab)-->
    <tabStrip>
      <tabStripItem>
        <label text="News" />
      </tabStripItem>
      <tabStripItem class="special">
        <label text="Sport" />
      </tabStripItem>
      <tabStripItem class="special">
        <label text="Culture" />
      </tabStripItem>
    </tabStrip>

    <!-- The number of TabContentItem components should corespond to the number of TabStripItem components -->
    <tabContentItem>
      <gridLayout>
        <Articles articles={news} />
      </gridLayout>
    </tabContentItem>
    <tabContentItem>
      <gridLayout>
        <Articles articles={sport} />
      </gridLayout>
    </tabContentItem>
    <tabContentItem>
      <gridLayout>
        <Articles articles={culture} />
      </gridLayout>
    </tabContentItem>

  </tabs>
</page>
