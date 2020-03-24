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
This is a single page application. Everything is handled in app/App.svelte. This file...
- fetches data from firestore in the svelte <a href='https://svelte-native.technology/docs#property-element'>onMount</a> function
- uses a <a href='https://svelte-native.technology/docs#scrollview'>scrollView</a> to display the list of items
- uses <a href='https://svelte-native.technology/docs#showmodal'>Modal</a> to show the full article
- you are not able to do anything further with the items - i.e delete, update or add - so the example just serves as a demo of how you can include firestore in a simple svelt native application
