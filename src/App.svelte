<script lang="ts">
  import Greet from "./lib/Greet.svelte";
  import { Alert } from "flowbite-svelte";
  import {
    Footer,
    FooterBrand,
    FooterCopyright,
    FooterIcon,
    FooterLink,
    FooterLinkGroup,
  } from "flowbite-svelte";
  import { onMount } from "svelte";
  import {
    DarkMode,
    Navbar,
    NavBrand,
    NavLi,
    NavUl,
    NavHamburger,
    Drawer,
    CloseButton,
    Sidebar,
    SidebarBrand,
    SidebarCta,
    SidebarDropdownItem,
    SidebarDropdownWrapper,
    SidebarGroup,
    SidebarItem,
    SidebarWrapper,
  } from "flowbite-svelte";
  import { sineIn } from "svelte/easing";

  let transitionParams = {
    x: -320,
    duration: 200,
    easing: sineIn,
  };

  let breakPoint: number = 1024;
  let width: number;
  let backdrop: boolean = false;
  let activateClickOutside = true;
  let drawerHidden: boolean = false;
  $: if (width >= breakPoint) {
    drawerHidden = false;
    activateClickOutside = false;
  } else {
    drawerHidden = true;
    activateClickOutside = true;
  }
  onMount(() => {
    if (width >= breakPoint) {
      drawerHidden = false;
      activateClickOutside = false;
    } else {
      drawerHidden = true;
      activateClickOutside = true;
    }
  });
  const toggleSide = () => {
    if (width < breakPoint) {
      drawerHidden = !drawerHidden;
    }
  };
  const toggleDrawer = () => {
    drawerHidden = false;
  };

  let spanClass =
    "pl-2 self-center text-md text-gray-900 whitespace-nowrap dark:text-white";
  let darkmodebtn =
    "text-gray-500 dark:text-gray-400 hover:bg-gray-100 dark:hover:bg-gray-700 focus:outline-none focus:ring-4 focus:ring-gray-200 dark:focus:ring-gray-700 rounded-lg text-lg p-2.5 fixed right-2 top-12  md:top-3 md:right-2 z-50";
  let divClass = "w-full md:block md:w-auto pr-8";
  let ulClass =
    "flex flex-col p-4 mt-4 md:flex-row md:space-x-8 md:mt-0 md:text-lg md:font-medium";
</script>

<svelte:window bind:innerWidth={width} />

<Navbar let:hidden let:toggle>
  <NavHamburger on:click={toggleDrawer} btnClass="ml-3 lg:hidden" />
  <NavBrand href="/" class="lg:ml-64">
    <span
      class="self-center whitespace-nowrap text-xl font-semibold dark:text-white pl-4"
    >
      My Website
    </span>
  </NavBrand>
  <NavHamburger on:click={toggle} />
  <NavUl {hidden} {divClass} {ulClass}>
    <NavLi href="/">Home</NavLi>
    <NavLi href="/pages/about">About</NavLi>
    <NavLi
      href="https://github.com/shinokada/flowbite-sveltekit-responsive-sidebar-layout"
      >GitHub</NavLi
    >
  </NavUl>
</Navbar>
<DarkMode btnClass={darkmodebtn} />
<Drawer
  transitionType="fly"
  {backdrop}
  {transitionParams}
  bind:hidden={drawerHidden}
  bind:activateClickOutside
  width="w-64"
  class="overflow-scroll pb-32"
  id="sidebar"
>
  <div class="flex items-center">
    <CloseButton
      on:click={() => (drawerHidden = true)}
      class="mb-4 dark:text-white lg:hidden"
    />
  </div>
  <Sidebar asideClass="w-54">
    <SidebarWrapper
      divClass="overflow-y-auto py-4 px-3 rounded dark:bg-gray-800"
    >
      <SidebarGroup>
        <SidebarItem label="Home" href="/" on:click={toggleSide} />
        <SidebarItem
          label="About"
          href={`/pages/`}
          {spanClass}
          on:click={toggleSide}
        />
        <SidebarItem label="Dashboard">
          <svelte:fragment slot="icon">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              class="w-6 h-6"
              ><path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M10.5 6a7.5 7.5 0 107.5 7.5h-7.5V6z"
              /><path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M13.5 10.5H21A7.5 7.5 0 0013.5 3v7.5z"
              /></svg
            >
          </svelte:fragment>
        </SidebarItem>
      </SidebarGroup>
    </SidebarWrapper>
  </Sidebar>
</Drawer>

<div class="flex px-4 mx-auto w-full">
  <main class="lg:ml-72 w-full mx-auto">
    <Greet />
  </main>
</div>

<style>
</style>
