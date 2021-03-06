<script>
  import Icon from "@/components/icons/Icon.svelte";
  import { darkTheme } from "@/stores/stores.js";

  function setTheme() {
    try {
      darkTheme.update((n) => !n);
      if ($darkTheme) {
        document.documentElement.classList.add("dark");
      } else {
        document.documentElement.classList.remove("dark");
      }
    } catch (error) {
      console.log(error);
    }
  }

  let hide = "true";

  let menuItems = [
    { link: "/", name: "Home", rel: "prerender", target: "_self" },
    {
      link: "https://github.com/HAUDRAUFHAUN/eduteam",
      name: "GitHub",
      rel: "noopener",
      target: "_blank",
    },
  ];
</script>

<div class="max-w-full mx-auto focus-within">
  <div
    class="relative z-10 pb-2 bg-indigo-500 sm:py-4 md:py-6 lg:max-w-full lg:w-full "
  >
    <div class="relative px-4 pt-2 sm:px-6 lg:px-8">
      <nav
        class="relative flex items-center justify-between sm:h-10 lg:justify-start lg:w-full"
        aria-label="Global"
      >
        <div class="hidden md:flex md:ml-10 md:pr-4 md:space-x-8">
          {#each menuItems as item}
            {#if item.name === "GitHub"}
              <a
                rel={item.rel}
                target={item.target}
                href={item.link}
                class="flex flex-row p-2 font-medium text-white rounded-md hover:text-indigo-800 hover:bg-indigo-300 dark:text-white dark:hover:text-white"
              >
                <span class="icon-wrapper"
                  ><Icon name="brand-github" />{item.name}</span
                ></a
              >
            {:else}
              <a
                rel={item.rel}
                target={item.target}
                href={item.link}
                class="flex flex-row p-2 font-medium text-white rounded-md hover:text-indigo-800 hover:bg-indigo-300 dark:text-white dark:hover:text-white"
                >{item.name}</a
              >
            {/if}
          {/each}
          <button
            class="absolute right-0 p-1 rounded-lg fill-current text-gray-50 hover:bg-gray-100 hover:text-gray-900 focus:outline-none"
            on:click={() => setTheme()}
            aria-label="change theme"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-7 w-7"
              width="24"
              height="24"
              viewBox="0 0 24 24"
              stroke-width="2"
              stroke="currentColor"
              fill="none"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <path stroke="none" d="M0 0h24v24H0z" fill="none" />
              <path d="M6.8 11a6 6 0 1 0 10.396 0l-5.197 -8l-5.2 8z" />
              <path d="M12 3v17" />
              <path d="M12 12l3.544 -3.544" />
              <path d="M12 17.3l5.558 -5.558" />
            </svg>
          </button>
        </div>
      </nav>
    </div>

    <!--
		  Mobile menu, show/hide based on menu open state.
  
		  Entering: "duration-150 ease-out"
			From: "opacity-0 scale-95"
			To: "opacity-100 scale-100"
		  Leaving: "duration-100 ease-in"
			From: "opacity-100 scale-100"
			To: "opacity-0 scale-95"
		-->
    <div class="right-0 md:hidden">
      <div class:hidden={hide === "false"}>
        <div class="flex items-center justify-between px-4">
          <div class="-m3-2">
            <button
              on:click={() => (hide = "false")}
              class="inline-flex items-center p-2 text-gray-400 bg-white rounded-md focus:outline-none dark:bg-gray-800 dark:text-white hover:bg-gray-100 dark:hover:bg-gray-700 focus:ring-2 focus:ring-inset focus:ring-indigo-500"
              aria-label="toggle mobile menu"
            >
              <svg
                class="w-6 h-6"
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M4 6h16M4 12h16M4 18h16"
                />
              </svg>
            </button>
          </div>
        </div>
      </div>
    </div>
    <div class:hidden={hide === "true"}>
      <div
        class="absolute inset-x-0 top-0 p-2 transition origin-top-right transform md:hidden"
      >
        <div
          class="overflow-hidden bg-white rounded-lg shadow-md dark:bg-gray-800 ring-1 ring-black ring-opacity-5"
        >
          <div class="flex items-center justify-between px-5 pt-4">
            <div class="-mr-2">
              <button
                type="button"
                on:click={() => (hide = "true")}
                class="inline-flex items-center justify-center p-2 text-red-500 bg-white rounded-md focus:outline-none dark:bg-gray-800 dark:text-red-300 hover:text-red-700 hover:bg-gray-100 focus:ring-2 focus:ring-inset focus:ring-indigo-500"
                aria-label="close mobile menu"
              >
                <span class="sr-only">Close main menu</span>
                <!-- Heroicon name: x -->
                <svg
                  class="w-6 h-6"
                  xmlns="http://www.w3.org/2000/svg"
                  fill="none"
                  viewBox="0 0 24 24"
                  stroke="currentColor"
                  aria-hidden="true"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M6 18L18 6M6 6l12 12"
                  />
                </svg>
              </button>
            </div>
          </div>
          <div
            role="menu"
            aria-orientation="vertical"
            aria-labelledby="main-menu"
          >
            <div class="px-2 pt-2 pb-3 space-y-1" role="none">
              {#each menuItems as item}
                <a
                  href={item.link}
                  class="block px-3 py-2 text-base font-medium text-gray-700 rounded-md hover:text-gray-900 hover:bg-gray-50 dark:text-white dark:bg-gray-800 dark:hover:bg-gray-600"
                  role="menuitem">{item.name}</a
                >
              {/each}
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<style>
</style>
