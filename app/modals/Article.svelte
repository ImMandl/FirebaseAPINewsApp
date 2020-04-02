<script>
  import { closeModal } from "svelte-native";
  import { navigate } from "svelte-native";
  export let article;

  import * as SocialShare from "nativescript-social-share";

  // funksjon for å dele tekst
  // krasjer appen
  const shareText = () => {
    socialShareModule.shareText(
      "Look at this article!",
      "How would you like to share this text?"
    );
    console.log("deling av artikkel");
  };
</script>

<style>
  .main {
    background-color: #eee;
  }
  .bilde {
    margin-bottom: 16;
    width: 100%;
  }
  .ingress {
    font-weight: bold;
    font-size: 16;
    margin: 16 0;
    line-height: 4;
    color: #292b33;
  }
  .brodtekst {
    font-size: 16;
    line-height: 4;
    color: #292b33;
  }
  .h1 {
    color: #292b33;
  }
</style>

<frame>
  <page class="main">
    <scrollView>
      <stackLayout>
        <image
          src={article.fields.url}
          class="bilde"
          alt="article image"
          stretch="aspectFit" />
        <stackLayout padding="24">
          <label textWrap="true" class="h1" text={article.fields.tittel} />
          <button on:tap={shareText} text="Del" />
          <label
            textWrap="true"
            class="ingress"
            text={article.fields.ingress} />
          <label
            textWrap="true"
            class="brodtekst"
            text={article.fields.tekst} />
          <button on:tap={() => closeModal()} text="Tilbake" />
        </stackLayout>
      </stackLayout>
    </scrollView>
  </page>
</frame>
