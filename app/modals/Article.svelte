<script>
  import { closeModal } from "svelte-native";
  export let article;
</script>

<style>
  .bilde {
    margin-bottom: 16;
  }
  .ingress {
    font-weight: bold;
    font-size: 16;
    margin: 16 0;
    line-height: 18;
  }
  .brodtekst {
    font-size: 14;
    line-height: 16;
  }
</style>

<frame>
  <page>
    <scrollView>
      <stackLayout style="padding:24">
        <image
          src={article.fields.url}
          class="bilde"
          alt="article image"
          stretch="aspectFit" />
        <label textWrap="true" class="h1" text={article.fields.tittel} />
        <label textWrap="true" class="ingress" text={article.fields.ingress} />
        <label textWrap="true" class="brodtekst" text={article.fields.tekst} />
        <button on:tap={() => closeModal()} text="Tilbake" />
      </stackLayout>
    </scrollView>
  </page>
</frame>
