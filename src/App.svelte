<script lang="ts">
  import Hls from 'hls.js';
  import { onMount } from 'svelte';
  import map from './map.png';

  let northup136: HTMLVideoElement;
  let spring136: HTMLVideoElement;
  let spring132: HTMLVideoElement;
  let se8112: HTMLVideoElement;

  const initStream = (url: string, video: HTMLVideoElement) => {
    if (video.canPlayType('application/vnd.apple.mpegurl')) {
      video.src = url;
    } else if (Hls.isSupported()) {
      const hls = new Hls({});
      hls.loadSource(url);
      hls.attachMedia(video);
      hls.on(Hls.Events.MANIFEST_PARSED, () => video.play());
    }
  };

  onMount(() => {
    initStream(
      'https://trafficcams.bellevuewa.gov/traffic-edge/CCTV185L.stream/chunklist_w1258849135.m3u8',
      northup136
    );
    initStream(
      'https://trafficcams.bellevuewa.gov/traffic-edge/CCTV199L.stream/chunklist_w1371433698.m3u8',
      spring136
    );
    initStream(
      'https://trafficcams.bellevuewa.gov/traffic-edge/CCTV197L.stream/chunklist_w1860076584.m3u8',
      spring132
    );
    initStream(
      'https://trafficcams.bellevuewa.gov/traffic-edge/CCTV089L.stream/chunklist_w830562892.m3u8',
      se8112
    );
  });
</script>

<div>
  <!-- svelte-ignore a11y-media-has-caption -->
  <video muted autoplay bind:this={northup136}></video>
  <video muted autoplay bind:this={spring136}></video>
  <video muted autoplay bind:this={se8112}></video>
  <video muted autoplay bind:this={spring132}></video>
</div>

<style>
  div {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-gap: 0;
  }
  video {
    width: 100%;
    height: 100%;
  }
</style>
