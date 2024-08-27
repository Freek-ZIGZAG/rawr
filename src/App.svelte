<script lang="ts">

    import {onMount} from "svelte";

    const sound = '/rawr.mp3';
    let playing = false;
    let audio: HTMLAudioElement;

    onMount(() => {
        audio = new Audio(sound);
    });

    function is_playing() {
        return audio && !audio.paused;
    }

    function play_sound() {
        if (!audio) return;
        if (is_playing()) {
            audio.pause();
            audio.currentTime = 0;
        }
        audio.play();
        playing = true;

        setTimeout(() => {
            playing = false;
        }, 1500);
    }
</script>

<main>
    <button  class="big-red-btn"
             class:playing
        on:click={play_sound}
    >
        <div class="big-red-btn__text">
            RAWR
        </div>
    </button>
</main>

<style lang="scss">
    main {
      @apply flex-1 flex justify-center items-center;
    }

    .big-red-btn {
      width: 200px;
        height: 200px;
      @apply bg-red-500 text-white font-bold text-2xl p-4 rounded-full flex justify-center items-center relative transform;
      transition: all 2s;

      &:before {
        // border around the button
        content: '';
        @apply absolute inset-0 border-4 border-white rounded-full;
      }

        &.playing {
          @apply  scale-150
        }
    }
</style>
