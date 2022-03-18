<template>
  <div class="bg-dark h-screen">
    <!-- Container -->
    <div class="flex" style="height: 88vh">
      <!-- side nav -->
      <div
        class="w-56 bg-black h-full flex-none overflow-y-scroll overflow-x-hidden scrollbar"
      >
        <div class="p-6">
          <img
            src="./assets/spotifylogo.png"
            alt="spotify"
            class="h-10"
            style="filter: brightness(0) invert(1)"
          />
        </div>
        <div class="mx-2 mb-5">
          <button
            v-for="page in pages"
            :key="page.id"
            @click="setID = page.id"
            :class="`w-full text-s font-semibold rounded px-3 py-2 flex items-center justify-start  ${
              setID === page.id
                ? ' bg-light text-white'
                : 'text-lightest hover:text-slate-300'
            }`"
          >
            <i class="material-icons mr-3">{{ page.icon }}</i>
            <p>{{ page.name }}</p>
          </button>
        </div>
        <div class="mx-5">
          <h1 class="text-xs mb-3 text-lightest tracking-widest uppercase">Playlists</h1>
          <button class="flex items-center justify-start opacity-75 hover:opacity-100">
            <img src="./assets/addNew.png" alt="addNew" class="h-7 w-7 mr-3 bg-white" />
            <p class="text-white font-semibold text-sm">Add New</p>
          </button>
          <button
            class="flex items-center justify-start opacity-75 hover:opacity-100 mt-3"
          >
            <img
              src="./assets/favorite1.png"
              alt="addNew"
              class="h-7 w-7 mr-3 bg-gradient-to-br from-fromcolor to-tocolor"
            />
            <p class="text-white font-semibold text-sm">Like Songs</p>
          </button>
        </div>
        <div class="h-px w-full bg-light my-7"></div>
        <div class="mx-5">
          <div class="w-full h-20 overflow-y-scroll text-lightest scrollbar">
            <p v-for="album in albums" class="px-7 py-2 text-sm hover:text-white">
              {{ album.name }}
            </p>
          </div>
          <button
            class="flex justify-center items-center text-lightest my-5 hover:text-white font-semibold"
          >
            <i class="material-icons mr-3 font-semibold">arrow_circle_down</i>
            <p class="font-semibold">Install App</p>
          </button>
        </div>
        <div class="relative">
          <div
            class="w-full h-full flex justify-end items-start p-3 pr-4 absolute opacity-0 hover:opacity-100"
          >
            <div class="bg-black rounded-full h-6 w-6">
              <i class="material-icons text-white">keyboard_arrow_down</i>
            </div>
          </div>
          <img src="./assets/playing.jpg" class="h-full w-full" />
        </div>
      </div>

      <!-- main content -->
      <div class="w-full h-full relative overflow-y-auto overflow-x-hidden scrollbar">
        <!-- header -->
        <div class="w-full sticky top-0 p-2 flex items-center justify-between mt-3 z-10">
          <div class="flex items-center ml-3">
            <button
              class="rounded-full h-8 w-8 bg-black text-white text-center flex items-center justify-center"
            >
              <i class="material-icons text-3xl">keyboard_arrow_left</i>
            </button>
            <button
              class="rounded-full h-8 w-8 bg-black text-white text-center flex items-center justify-center ml-3"
            >
              <i class="material-icons text-3xl">keyboard_arrow_right</i>
            </button>
          </div>
          <div class="relative mr-3">
            <button
              class="bg-light rounded-full p-1 flex items-center justify-around px-1"
              @click="showDropdown = !showDropdown"
            >
              <img src="./assets/resim.jpg" alt="myPic" class="rounded-full h-6 w-6" />
              <p class="text-white font-semibold text-xs mx-2">Kursat Karsli</p>
              <i class="material-icons w-8 text-white" v-if="!showDropdown"
                >arrow_drop_down</i
              >
              <i class="material-icons w-8 text-white" v-else>arrow_drop_up</i>
            </button>
            <div class="absolute bg-light p-2 w-full rounded mt-1" v-if="showDropdown">
              <button
                class="py-2 text-lightest hover:text-white border-b border-lightest w-full text-sm"
                @click="showDropdown = false"
              >
                Account
              </button>
              <button
                class="py-2 text-lightest hover:text-white border-b border-light w-full text-sm"
                @click="showDropdown = false"
              >
                Log Out
              </button>
            </div>
          </div>
        </div>
        <!-- Cards -->
        <div class="px-6 py-3 flex items-center justify-between">
          <h1 class="text-2xl font-semibold text-white tracking-wider hover:underline">
            Recently Played
          </h1>
          <h2 class="text-xs text-lightest uppercase tracking-wider hover:underline mr-9">
            See All
          </h2>
        </div>
        <div class="w-full flex flex-wrap gap-3 mx-5">
          <div v-for="recent in recents" class="p-2 w-48 relative">
            <div
              class="absolute w-full h-full flex items-end justify-end p-8 opacity-0 hover:opacity-100 transition-opacity duration-500"
            >
              <div
                class="bg-green rounded-full h-10 w-10 flex items-center justify-center"
              >
                <i class="material-icons">play_arrow</i>
              </div>
            </div>
            <div class="bg-light w-full h-auto p-5">
              <img
                :src="` ${recent.src} `"
                class="h-auto w-full shadow mb-2"
                :style="`${recent.title === 'Daily Mix 2' ? 'height: 136px' : null}`"
              />
              <h1 class="text-sm font-semibold text-white tracking-wide">
                {{ recent.title }}
              </h1>
              <h2 class="text-xs font-semibold text-lightest tracking-wide">
                {{ recent.artist }}
              </h2>
            </div>
          </div>
        </div>
        <div class="px-6 py-3 flex items-center justify-between">
          <h1 class="text-2xl font-semibold text-white tracking-wider hover:underline">
            Made For Kursat
          </h1>
          <h2 class="text-xs text-lightest uppercase tracking-wider hover:underline mr-9">
            See All
          </h2>
        </div>
        <div class="w-full flex flex-wrap gap-3 mx-5">
          <div v-for="yourmix in yourmixes" class="p-2 w-48 relative">
            <div
              class="absolute w-full h-full flex items-end justify-end p-8 opacity-0 hover:opacity-100 transition-opacity duration-500"
            >
              <div
                class="bg-green rounded-full h-10 w-10 flex items-center justify-center"
              >
                <i class="material-icons">play_arrow</i>
              </div>
            </div>
            <div class="bg-light w-full h-auto p-5">
              <img
                :src="` ${yourmix.src} `"
                class="h-auto w-full shadow mb-2"
                :style="`${yourmix.title === 'My Mix 2' ? 'height: 136px' : null}`"
              />
              <h1 class="text-sm font-semibold text-white tracking-wide">
                {{ yourmix.title }}
              </h1>
              <h2 class="text-xs font-semibold text-lightest tracking-wide">
                {{ yourmix.artist }}
              </h2>
            </div>
          </div>
        </div>
        <div class="px-6 py-3 flex items-center justify-between">
          <div>
            <h1 class="text-2xl font-semibold text-white tracking-wider hover:underline">
              More of what you like
            </h1>
            <p class="text-xs text-lightest tracking-wider hover:underline mr-9">
              Hear a little bit of everything you love.
            </p>
          </div>
          <h2 class="text-xs text-lightest uppercase tracking-wider hover:underline mr-9">
            SEE ALL
          </h2>
        </div>
        <div class="w-full flex flex-wrap gap-3 mx-5">
          <div v-for="yourmix in yourmixes" class="p-2 w-48 relative">
            <div
              class="absolute w-full h-full flex items-end justify-end p-8 opacity-0 hover:opacity-100 transition-opacity duration-500"
            >
              <div
                class="bg-green rounded-full h-10 w-10 flex items-center justify-center"
              >
                <i class="material-icons">play_arrow</i>
              </div>
            </div>
            <div class="bg-light w-full h-auto p-5">
              <img
                :src="` ${yourmix.src} `"
                class="h-auto w-full shadow mb-2"
                :style="`${yourmix.title === 'My Mix 2' ? 'height: 136px' : null}`"
              />
              <h1 class="text-sm font-semibold text-white tracking-wide">
                {{ yourmix.title }}
              </h1>
              <h2 class="text-xs font-semibold text-lightest tracking-wide">
                {{ yourmix.artist }}
              </h2>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- playbar -->
    <div
      class="w-full bg-light flex items-center justify-between px-3"
      style="height: 12vh"
    >
      <div class="flex items-center">
        <div>
          <h1 class="text-sm text-white tracking-wide">
            Summer in the City - Remastered
          </h1>
          <h2 class="text-xs text-lightest tracking-wider">The Lovin' Spoonful</h2>
        </div>
        <i class="material-icons text-xl text-green mx-4">favorite</i>
        <i class="material-icons text-xl text-lightest hover:text-white"
          >picture_in_picture_alt</i
        >
      </div>
      <div class="flex items-center flex-col justify-center w-1/2">
        <div class="w-full flex justify-center">
          <button class="text-lightest hover:text-white mx-5">
            <i class="material-icons text-xs"> shuffle</i>
          </button>
          <button class="text-lightest hover:text-white">
            <i class="material-icons text-xs" @click="resetTimeDuration()"
              >skip_previous</i
            >
          </button>
          <button class="text-lightest h-8 w-6 hover:text-white mx-5">
            <i
              v-if="pause === false"
              @click="playSong('../src/assets/song.mp3'), (pause = !pause)"
              class="material-icons text-xl"
              >play_circle_outlined</i
            >
            <i
              v-if="pause === true"
              @click="pauseSong(), (pause = !pause)"
              class="material-icons text-xl"
              >pause_circle_outlined
            </i>
          </button>
          <button class="text-lightest hover:text-white">
            <i class="material-icons text-xs">skip_next</i>
          </button>
          <button class="text-lightest hover:text-white mx-5">
            <i class="material-icons text-xs">loop</i>
          </button>
        </div>

        <div class="w-full flex items-center justify-center">
          <p class="text-xs font-semibold text-lightest pt-2">01:18</p>
          <div
            class="w-full bg-lightest mt-4 rounded-full h-1 hover:bg-white mx-3 flex items-center"
          >
            <div class="h-1 rounded-full bg-green" style="width: 18%"></div>
            <div class="h-2 w-2 bg-white rounded-full"></div>
          </div>
          <p class="text-xs font-semibold text-lightest pt-2 -ml-1 shadow">04:58</p>
        </div>
      </div>

      <div class="flex items-center">
        <svg
          role="img"
          height="16"
          width="16"
          viewBox="0 0 16 16"
          class="mr-2 fill-lightest hover:fill-white"
        >
          <path
            d="M 13.426 2.574 a 2.831 2.831 0 0 0 -4.797 1.55 l 3.247 3.247 a 2.831 2.831 0 0 0 1.55 -4.797 Z M 10.5 8.118 l -2.619 -2.62 A 63303.1 63303.1 0 0 0 4.74 9.075 L 2.065 12.12 a 1.287 1.287 0 0 0 1.816 1.816 l 3.06 -2.688 l 3.56 -3.129 Z M 7.12 4.094 a 4.331 4.331 0 1 1 4.786 4.786 l -3.974 3.493 l -3.06 2.689 a 2.787 2.787 0 0 1 -3.933 -3.933 l 2.676 -3.045 l 3.505 -3.99 Z"
          />
        </svg>
        <i class="material-icons text-2xl text-lightest hover:text-white"
          >playlist_play</i
        >
        <i class="material-icons text-xl text-lightest hover:text-white mx-3"
          >important_devices</i
        >

        <i class="material-icons text-xl text-lightest hover:text-white">volume_up</i>
        <div class="w-36 ml-3 bg-lightest rounded-full h-1 hover:bg-white"></div>
      </div>
    </div>
  </div>
</template>
<script>
// import song from '../src/assets/song.mp3';

export default {
  name: 'App',
  data() {
    return {
      pause: false,
      pages: [
        { id: 'home', name: 'Home', icon: 'home' },
        { id: 'search', name: 'Search', icon: 'search' },
        { id: 'library', name: 'Your Library', icon: 'bar_chart' },
      ],
      setID: '',
      showDropdown: false,
      albums: [
        { name: 'Drive' },
        { name: 'Legendary' },
        { name: 'Türk Kahvesi' },
        { name: 'Ezginin Günlüğü' },
        { name: 'Cevapsız Sorular' },
        { name: 'Soft Rock' },
      ],
      recents: [
        {
          src: 'https://pbs.twimg.com/media/CtcVNESWIAEYGWI?format=jpg&name=360x360',
          title: 'Daily Mix 1',
          artist: 'By Spotify',
        },
        {
          src: 'https://i.pinimg.com/564x/9a/41/98/9a4198abfd84448781ae162c4d8bd1a6.jpg',
          title: 'Daily Mix 2',
          artist: 'By Spotify',
        },
        {
          src:
            'https://dailymix-images.scdn.co/v2/img/ab6761610000e5ebdf4cd71f6606bd53e2c7eb5b/1/en/large',
          title: 'Daily Mix 3',
          artist: 'By Spotify',
        },
        {
          src:
            'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQiCxcjO8pODOun0sHBjqANAKaEwvU7XQy8Sot8p-NZpQRSZNeXbv_g9t7WFp3jDCPyRpc&usqp=CAU',
          title: 'Daily Mix 4',
          artist: 'By Spotify',
        },
        {
          src:
            'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRBxcAoO2HH-rJPB_bPqL7MhLriyug21KFtuw&usqp=CAU',
          title: 'Daily Mix 5',
          artist: 'By Spotify',
        },
        {
          src:
            'data:image/jpeg;base64,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',
          title: 'Daily Mix 6',
          artist: 'By Spotify',
        },
      ],
      yourmixes: [
        {
          src: 'https://pbs.twimg.com/media/CtcVNESWIAEYGWI?format=jpg&name=360x360',
          title: 'My Mix 1',
          artist: 'By Spotify',
        },
        {
          src: 'https://i.pinimg.com/564x/9a/41/98/9a4198abfd84448781ae162c4d8bd1a6.jpg',
          title: 'My Mix 2',
          artist: 'By Spotify',
        },
        {
          src:
            'https://dailymix-images.scdn.co/v2/img/ab6761610000e5ebdf4cd71f6606bd53e2c7eb5b/1/en/large',
          title: 'My Mix 3',
          artist: 'By Spotify',
        },
        {
          src:
            'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQiCxcjO8pODOun0sHBjqANAKaEwvU7XQy8Sot8p-NZpQRSZNeXbv_g9t7WFp3jDCPyRpc&usqp=CAU',
          title: 'My Mix 4',
          artist: 'By Spotify',
        },
        {
          src:
            'data:image/jpeg;base64,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',
          title: 'My Mix 5',
          artist: 'By Spotify',
        },
        {
          src:
            'data:image/jpeg;base64,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',
          title: 'My Mix 6',
          artist: 'By Spotify',
        },
      ],
      audio: new Audio(),
    };
  },
  methods: {
    playSong(song) {
      this.audio.src = song;
      this.audio.play();
    },
    pauseSong() {
      this.audio.pause();
    },
    resetTimeDuration() {
      this.audio.currentTime = 0;
    },
  },
};
</script>
<style scoped>
.scrollbar::-webkit-scrollbar {
  width: 15px;
}

.scrollbar::-webkit-scrollbar-track {
  border-radius: 50px;
  background: #282828;
}

.scrollbar::-webkit-scrollbar-thumb {
  background: #535353;
  border-radius: 50px;
  border: 3px solid #535353;
}

.scrollbar::-webkit-scrollbar-thumb:hover {
  background: rgb(211, 211, 211);
  border: 3px solid rgb(211, 211, 211);
}
</style>
