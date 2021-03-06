# Svelte native firestore app
This is a simple svelte native ANDROID/IOS app that uses a firebase/firstore API to create a news app. It connects using a fetch call to the build in REST API.

it uses the <a href='https://svelte-native.technology/docs'>svelte-native</a> framework to build a native application. Svelte native is built on top of <a href='https://nativescript.org'>Nativescritp</a>, so you need to go through the setup guide there in order to install the TNS CLI tools.

## Setup
```html
npm install
tns run [ios|android]
# or
tns preview
```

## Project structure
Articles list is handled in component/Articles.svelte while the full article is handled in modal/Article.svelte. app/App.svelte handles the navigate and displays the lists of article through component/Articles.svelte.

This file...
- uses <a href='https://docs.nativescript.org/ns-framework-modules/fetch'>fetch</a> to retrieve data from firestore and parse it through <a href='https://www.npmjs.com/package/firestore-parser'>firestore parser</a>.
```html
fetch(articlesUrl)
    .then(response => response.json())
    .then(json => FirestoreParser(json))
    .then(parsed => {
        news = parsed.documents.filter(art => art.fields.kategori == "nyhet");
        sport = parsed.documents.filter(art => art.fields.kategori == "sport");
        culture = parsed.documents.filter(art => art.fields.kategori == "kultur");
```
Firestore parser sends the different categories into their correspodning arrays:
```html
  let news = [];
  let sport = [];
  let culture = [];
```
which is then used in <a href='https://svelte-native.technology/docs#tabs'>tabs</a> to navigate between the different categories. They are all sent to component/Articles.svelte which then sends back the articles for only that category.
```html
  <tabs bind:selectedIndex={selectedTab}>

    <tabStrip>
      <tabStripItem>
        <label text="News" />
      </tabStripItem>
      <tabStripItem>
        <label text="Sport" />
      </tabStripItem>
      <tabStripItem>
        <label text="Culture" />
      </tabStripItem>
    </tabStrip>

    <tabContentItem>
        <Articles articles={news} />
    </tabContentItem>
    <tabContentItem>
        <Articles articles={sport} />
    </tabContentItem>
    <tabContentItem>
        <Articles articles={culture} />
    </tabContentItem>

  </tabs>
```
- uses a <a href='https://svelte-native.technology/docs#scrollview'>scrollView</a> to display the list of articles
- uses <a href='https://svelte-native.technology/docs#showmodal'>modal</a> to show the full article
- uses <a href='https://market.nativescript.org/plugins/nativescript-social-share'>NativeScript Social Share Plugin</a> to share either the article image or title
- you are not able to do anything further with the items - i.e delete, update or add. This app just simply lets you view articles fetched from firestore.

