<script>
  import { closeModal } from "svelte-native";
  import { navigate } from "svelte-native";
  export let article;

  import * as SocialShare from "nativescript-social-share";

  let image = "";
  let delTekst = "";

  // funksjon for å dele bilde
  const imageShare = () => {
    // setter hva som skal deles her så delingen ikke starter når article modal åpnes
    image = article.fields.url;
    SocialShare.shareImage(image);
  };

  // funksjon for å dele tekst
  const textShare = () => {
    // setter hva som skal deles her så delingen ikke starter når article modal åpnes
    delTekst = article.fields.tittel;
    SocialShare.shareText(delTekst, "How would you like to share this text?");
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
  .btn {
    padding: 8 12;
    margin: 0;
    margin-right: 8;
  }
  .back-btn {
    margin: 16 0;
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

          <flexboxLayout>
            <button class="btn" on:tap={imageShare} text="Del bilde" />
            <button class="btn" on:tap={textShare} text="Del overskrift" />
          </flexboxLayout>

          <label
            textWrap="true"
            class="ingress"
            text={article.fields.ingress} />
          <label
            textWrap="true"
            class="brodtekst"
            text={article.fields.tekst} />
          <button class="back-btn" on:tap={() => closeModal()} text="Tilbake" />
        </stackLayout>
      </stackLayout>
    </scrollView>
  </page>
</frame>
