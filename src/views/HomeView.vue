<template>
  <div class="full-width column items-center">
    <div class="full-width" style="height: 730px">
      <q-img
        class="fixed"
        style="height: 900px"
        src="../../public/Felix_nancybeygangphotography.jpg"
      ></q-img>
    </div>
    <div
      :class="
        'q-screen lt-lg'
          ? 'full-width q-pt-xl q-pb-xl bg-white row items-center justify-center text-black text-center'
          : 'full-width q-pt-xl q-pb-xl bg-white row items-center justify-center text-white text-center'
      "
      style="z-index: 1"
    >
      <div
        v-for="(item, index) in items"
        :key="index"
        class="col-4 col-sm-4 col-md-4 col-lg-2 column items-center justify-center img-container"
      >
        <q-img class="q-mb-md image" :src="item.src" />
        <span class="text-wrap">{{ item.label }}</span>
      </div>
    </div>
    <!-- Videoabschnitt -->
    <div
      class="video-container bg-white column full-width text-center"
      ref="videoSection"
      :class="{ 'is-visible': isVideoVisible }"
      style="z-index: 1"
    >
      <video ref="video" style="width: 100%; height: auto" muted loop>
        <source src="/Kvell Apparel Co. - Clothing Brand Promo Video.mp4" type="video/mp4" />
      </video>
      <p class="absolute-center column text-white">
        <span
          style="font-family: MontserratExtraBold"
          :class="$q.screen.lt.md ? 'text-h5' : 'text-h1'"
          >SALE </span
        ><span :class="$q.screen.lt.md ? 'text-h7' : 'text-h1'">MIT BIS ZU -50%</span
        ><span
          :class="$q.screen.lt.md ? 'text-h7' : 'text-h5'"
          style="font-family: MontserratSemiBold"
          >Auf ausgewählte Artikel</span
        >
      </p>
    </div>
    <div
      class="bg-white column full-width text-center"
      :style="$q.screen.lt.md ? 'z-index: 1; height: 550px' : 'z-index: 1; height: 800px'"
    >
      <span style="font-family: LexendBold" class="q-mt-lg text-h2 text-red">SALES</span
      ><span style="font-family: LexendBold" class="text-h5 q-mt-lg"
        >Weazel News! Here you will definetly find something for you.</span
      >
      <div class="row justify-center q-gutter-x-xl q-mt-xl">
        <div class="col-4 col-sm-3">
          <div class="img-container">
            <q-img
              class="image"
              src="/unisex-basic-softstyle-t-shirt-black-right-front-602c03dcdb607_1200x1200.webp"
              alt="Herren T-shirt"
            ></q-img>
          </div>
          <span class="text-h5">Herren</span>
        </div>
        <div class="col-4 col-sm-3">
          <div class="img-container">
            <q-img
              class="image"
              src="/damen-strickfleece-jacke-oesterreich_1400x.webp"
              alt="Damen Strickfleece"
            ></q-img>
          </div>
          <span class="text-h5">Damen</span>
        </div>
      </div>
    </div>
    <div
      class="bg-white row full-width text-center justify-center q-pt-xl"
      style="z-index: 1; height: 550px; border-top: 1px solid lightgray"
    >
      <div class="col-2 column items-start">
        <span class="text-h6 q-mb-md">Hilfe</span>
        <p class="column items-start text-blue-grey-5 q-gutter-y-md text-caption">
          <span>Häufig gestellte Fragen</span>
          <span>Status meiner Bestellung</span>
          <span>Rückgabevorgang</span>
          <span>Rückgabe bearbeiten</span>
        </p>
      </div>
      <div class="col-1 column items-start">
        <span class="text-h6 q-mb-md">Unternehmen</span>
        <p class="column items-start text-blue-grey-5 q-gutter-y-md text-caption">
          <span>Über uns</span>
          <span>Filialsuche</span>
          <span>Franchising</span>
          <span>Karriere</span>
        </p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

// Definiere ein Array von Artikeln mit Beschreibungen und Bildquellen
const items = [
  { label: 'Jeans & Hosen', src: '/hose_damen_eisk_gele_1.png' },
  { label: 'T-Shirts', src: '/f6f03570-fd7e-4ab5-b190-db8496381e16.avif' },
  { label: 'Unterwäsche', src: '/nads-boxer-briefs_grande.webp' },
  { label: 'Jacken & Mäntel', src: '/jacket_blackgold-600x600.png' },
  { label: 'Accessoires', src: '/2fde97d7e9081a843c3f728d4e9e-600x600.png' },
  { label: 'Taschen', src: '/PP3842K_41_dunkelblau_600x600.png' },
];

// Initialisiere Referenzen für das Video und den Videoabschnitt
const video = ref(null);
const videoSection = ref(null);

// Zustand, um zu verfolgen, ob der Videoabschnitt sichtbar ist
const isVideoVisible = ref(false);

// Deklariere einen Beobachter, um im onUnmounted verfügbar zu sein
let observer;

onMounted(() => {
  // Erstelle einen IntersectionObserver, um die Sichtbarkeit des Videoabschnitts zu überwachen
  observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        // Wenn der Abschnitt im Blickfeld ist, das Video abspielen und sichtbar machen
        if (entry.isIntersecting) {
          isVideoVisible.value = true;
          video.value.play();
        } else {
          // Pausiere das Video, wenn es nicht im Blickfeld ist
          isVideoVisible.value = false;
          video.value.pause();
        }
      });
    },
    { threshold: 0.5 }, // Beginne mit der Überwachung, wenn 50 % des Abschnitts sichtbar sind
  );

  // Beginne die Beobachtung des Videoabschnitts
  if (videoSection.value) {
    observer.observe(videoSection.value);
  }
});
</script>

<style lang="scss" scoped>
// Bildübergangseffekt
.image {
  transition: transform 0.3s ease-in-out;
  object-fit: cover;
  object-position: center;
  max-width: 100%;
  max-height: 100%;
}

// Verkleinere das Bild bei Hover
.img-container:hover .image {
  transform: scale(0.9);
}

// Video-Container-Effekt
.video-container {
  position: relative;
  transition: opacity 1s ease-in-out;
  background-color: #f0f0f0; // Stellt sicher, dass der Hintergrund immer grau ist, wenn das Video nicht sichtbar ist
}
</style>
