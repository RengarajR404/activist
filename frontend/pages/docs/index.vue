<template>
  <div
    class="text-light-text dark:text-dark-text bg-light-content dark:bg-dark-content"
  >
    <Head>
      <Title>{{ $t("pages.docs.index.title") }}</Title>
    </Head>
    <div class="bg-light-distinct dark:bg-dark-distinct">
      <div class="responsive-py-4 flex flex-col w-full responsive-px-5">
        <HeaderAppPage
          :header="$t('pages.docs.index.header')"
          :tagline="$t('pages.docs.index.subheader')"
        />
      </div>
    </div>
    <div class="responsive-py-5 responsive-px-5">
      <h3 class="transition-all duration-500 responsive-h2">
        {{ $t("pages.docs.index.section-1-subheader") }}
      </h3>
      <p
        class="responsive-py-1 text-light-special-text dark:text-dark-special-text"
      >
        {{ $t("pages.docs.index.section-1-tagline") }}
      </p>
      <GridDocEntries class="responsive-py-1" :cards="cards" />
    </div>
  </div>
</template>

<script setup lang="ts">
import type { CardDocsEntry } from "../../types/card-docs-entry";

const cards: CardDocsEntry[] = [
  {
    url: "get-active",
    title: "pages.docs.index.get-active",
    description: "pages.docs.index.get-active-description",
    imgURL: "/images/content_pages/art/get_active",
    imgDimensions: "h-20 sm:h-24",
    imgAltText: "pages.docs.index.get-active-alt-text",
  },
  {
    url: "get-organized",
    title: "pages.docs.index.get-organized",
    description: "pages.docs.index.get-organized-description",
    imgURL: "/images/content_pages/art/get_organized",
    imgDimensions: "h-16 sm:h-20",
    imgAltText: "pages.docs.index.get-organized-alt-text",
  },
  {
    url: "grow-organization",
    title: "pages.docs.index.grow-organization",
    description: "pages.docs.index.grow-organization-description",
    imgURL: "/images/content_pages/art/grow_organization",
    imgDimensions: "h-16 sm:h-20",
    imgAltText: "pages.docs.index.grow-organization-alt-text",
  },
];
</script>
