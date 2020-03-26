<script>
  import { closeModal } from "svelte-native";
  export let article;
</script>

<style>
  .main {
    background-color: #eee;
  }
  .main-inner {
    padding: 0 24 24 24;
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
