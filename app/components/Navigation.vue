
<template>
  <header class="fixed top-0 left-0 w-full z-[9999]">
    <div
      ref="containerEl"
      class="relative mx-auto h-[80px] flex items-center overflow-hidden"
      :style="isSticky
        ? { width: '100%', borderRadius: '0', marginTop: '0', paddingInline: isMobile ? '15px' : 'calc(7.5% + 15px)' }
        : isMobile
          ? { width: '100%', borderRadius: '0', marginTop: '0', paddingInline: '15px' }
          : { width: '85%', borderRadius: '40px', marginTop: '20px', paddingInline: '15px' }"
      :class="isSticky
        ? 'bg-white/60 shadow-[0_10px_15px_rgba(0,0,0,0.05)] backdrop-blur-[10px]'
        : 'bg-white/10 backdrop-blur-[2.5px] '"
      @mouseleave="onLeave"
    >

      <!-- White pill — spans full container by default, contracts to hovered nav link -->
      <span
        aria-hidden="true"
        class="absolute top-1/2 left-0 pointer-events-none"
        :class="[ready ? 'nav-slide' : 'opacity-0', isSticky ? 'shadow-[0_1px_8px_rgba(0,0,0,0.08)]' : 'shadow-[0_2px_14px_rgba(0,0,0,0.35)]', hoverIdx !== null ? 'bg-white/30' : 'bg-white/30']"
        :style="{
          width: pillW + 'px',
          height: pillH + 'px',
          transform: `translateX(${pillX}px) translateY(-50%)`,
          borderRadius: (isSticky && hoverIdx === null) ? '0px' : '40px'
        }"
      ></span>

      <!-- Logo -->
      <a href="#" class="relative shrink-0 no-underline z-10">
        <img :src="logoScroll" alt="Staco" class="h-9 w-auto" />
      </a>

      <!-- Nav links -->
      <div class="flex items-center ml-8 max-[991px]:hidden">
        <ul
          ref="navEl"
          role="tablist"
          aria-label="Main navigation"
          class="flex items-center list-none m-0 p-0"
          @keydown="onKey"
          @focusout="onNavFocusOut"
        >
          <li
            v-for="(item, i) in navItems" :key="item"
            role="tab"
            tabindex="0"
            :aria-selected="i === activeIdx"
            class="relative z-10 cursor-pointer rounded-[30px] outline-none nav-tab"
            @mouseenter="onHover($event, i)"
            @focus="onTabFocus(i)"
            @click="onSelect($event, i)"
          >
            <!-- Per-tab indicator — inset-y-[3px] keeps it shorter than full li height -->
            <span
              aria-hidden="true"
              class="absolute inset-x-0 inset-y-[3px] rounded-[30px] pointer-events-none transition-all duration-150"
              :class="i === activeIdx ? 'bg-white shadow-[0_1px_6px_rgba(0,0,0,0.12)]' : ''"
            ></span>
            <span
              class="relative flex items-center gap-1 px-4 py-[7px] text-[15px] whitespace-nowrap select-none transition-colors duration-150"
              :class="i === activeIdx ? 'font-bold text-[#1a1a1a]'
                : i === targetIdx ? 'font-semibold text-[#1a1a1a]'
                : ' text-black'"
            >
              {{ item }}
              <svg v-if="item === 'Home' || item === 'Pages'" class="w-2.5 h-[6px] shrink-0 ml-0.5" viewBox="0 0 10 6" fill="none">
                <path d="M1 1l4 4 4-4" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
              </svg>
            </span>
          </li>
        </ul>
      </div>

      <!-- Spacer -->
      <div class="flex-1 max-[991px]:hidden"></div>

      <!-- Right actions — EN + Sign in + Start Free -->
      <div class="relative z-10 flex items-center gap-1 max-[991px]:hidden">
        <a href="#" class="flex items-center gap-1.5 text-sm font-medium px-3 py-[7px] rounded-[30px] no-underline text-[#1f2334]/60 transition-colors duration-100 hover:bg-black/[0.06]">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" class="w-4 h-4 shrink-0">
            <circle cx="12" cy="12" r="10"/><path d="M2 12h20M12 2a15.3 15.3 0 010 20M12 2a15.3 15.3 0 000 20"/>
          </svg>
          EN
        </a>
        <a href="#" class="relative z-10 text-[15px] font-semibold px-3 py-[7px] rounded-[30px] no-underline text-[#1f2334]/60 transition-colors duration-100 hover:bg-black/[0.06]">
          Sign in
        </a>
        <a href="#" class="h-9 px-5 bg-[#B2EDA1] text-[#1f2334] text-sm font-bold rounded-full flex items-center whitespace-nowrap no-underline transition-[background,color] duration-200 hover:bg-[#44C486] hover:text-white">
          Start Free
        </a>
      </div>

      <!-- Mobile burger -->
      <button
        class="relative z-10 hidden max-[991px]:flex items-center justify-center bg-transparent border-0 cursor-pointer w-8 h-8 p-0 transition-colors duration-300 ml-auto text-[#1f2334]"
        @click="mobileOpen = !mobileOpen"
      >
        <svg v-if="!mobileOpen" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" class="w-6 h-6">
          <path d="M4 6h16M4 12h16M4 18h16" stroke-linecap="round"/>
        </svg>
        <svg v-else viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" class="w-6 h-6">
          <path d="M6 18L18 6M6 6l12 12" stroke-linecap="round"/>
        </svg>
      </button>
    </div>

    <!-- Mobile menu overlay — desktop hidden via CSS -->
    <div v-if="mobileOpen" class="hidden max-[991px]:flex flex-col bg-white fixed top-0 left-0 right-0 bottom-0 z-[9998] overflow-y-auto">
      <!-- Header: logo + close -->
      <div class="flex items-center justify-between px-6 h-[80px] shrink-0 border-b border-black/[.06]">
        <img :src="logoScroll" alt="Staco" class="h-9 w-auto" />
        <button
          class="w-9 h-9 flex items-center justify-center rounded-full bg-black/[.05] border-0 cursor-pointer text-[#1f2334]"
          @click="mobileOpen = false"
          aria-label="Close menu"
        >
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" class="w-5 h-5">
            <path d="M6 18L18 6M6 6l12 12" stroke-linecap="round"/>
          </svg>
        </button>
      </div>
      <!-- Nav links -->
      <div class="flex flex-col gap-1 p-6">
        <a v-for="item in navItems" :key="item" href="#"
          class="px-4 py-3 text-[15px] font-medium text-[#1f2334] rounded-xl hover:bg-gray-50 no-underline">
          {{ item }}
        </a>
        <div class="flex gap-3 px-4 pt-4 items-center">
          <a href="#" class="text-[15px] font-semibold text-[#1f2334] no-underline">Sign in</a>
          <a href="#" class="h-10 px-6 bg-[#B2EDA1] text-[#1f2334] text-sm font-bold rounded-full flex items-center transition-colors hover:bg-[#44C486] hover:text-white no-underline">Start Free</a>
        </div>
      </div>
    </div>
  </header>
</template>

<script setup>
import logoScroll from '~/assets/images/icons/logoscroll.png'

const isSticky   = ref(false)
const isMobile   = ref(false)
const mobileOpen = ref(false)
const navItems   = ['Home', 'Pages', 'Services', 'Blogs', 'Contact Us']
const activeIdx  = ref(0)
const hoverIdx   = ref(null)
const kbIdx      = ref(null)   // tab focused via keyboard (null = no keyboard focus in tablist)
const targetIdx  = computed(() => hoverIdx.value ?? kbIdx.value ?? activeIdx.value)

// ── Pill (full container → contracts to hovered nav link) ─────────────────────
const containerEl = ref(null)
const navEl       = ref(null)
const pillX       = ref(0)
const pillW       = ref(0)
const pillH       = ref(0)
const ready       = ref(false)

const GAP        = 5
const TAB_H      = 36  // h-9

const measureFull = () => {
  if (!containerEl.value) return
  if (hoverIdx.value === null && kbIdx.value === null) {
    pillX.value = GAP
    pillW.value = containerEl.value.offsetWidth - GAP * 2
    pillH.value = containerEl.value.offsetHeight - GAP * 2
  }
}

const onHover = (e, i) => {
  hoverIdx.value = i
  const rect          = e.currentTarget.getBoundingClientRect()
  const containerRect = containerEl.value.getBoundingClientRect()
  pillX.value = rect.left - containerRect.left
  pillW.value = rect.width
  pillH.value = TAB_H
}

const onLeave = () => {
  hoverIdx.value = null
  pillX.value = GAP
  pillW.value = (containerEl.value?.offsetWidth ?? 0) - GAP * 2
  pillH.value = (containerEl.value?.offsetHeight ?? 0) - GAP * 2
}

const onSelect = (e, i) => {
  activeIdx.value = i
  hoverIdx.value  = null
  pillX.value = GAP
  pillW.value = (containerEl.value?.offsetWidth ?? 0) - GAP * 2
  pillH.value = (containerEl.value?.offsetHeight ?? 0) - GAP * 2
}

// keyboard: shrink pill to focused item
const measureAt = (i) => {
  const el = navEl.value?.querySelectorAll('[role="tab"]')[i]
  if (!el || !containerEl.value) return
  const rect = el.getBoundingClientRect()
  pillX.value = rect.left - containerEl.value.getBoundingClientRect().left
  pillW.value = rect.width
  pillH.value = TAB_H
}

const expandPill = () => {
  pillX.value = GAP
  pillW.value = (containerEl.value?.offsetWidth ?? 0) - GAP * 2
  pillH.value = (containerEl.value?.offsetHeight ?? 0) - GAP * 2
}

const onTabFocus = (i) => {
  kbIdx.value = i
  measureAt(i)
}

const onNavFocusOut = (e) => {
  // Only reset when focus leaves the tablist entirely
  if (!navEl.value?.contains(e.relatedTarget)) {
    kbIdx.value = null
    if (hoverIdx.value === null) expandPill()
  }
}

const onKey = (e) => {
  const n = navItems.length
  const curr = kbIdx.value ?? activeIdx.value

  // Activate focused tab
  if (e.key === 'Enter' || e.key === ' ') {
    e.preventDefault()
    activeIdx.value = curr
    return
  }

  const nextMap = {
    ArrowRight: (curr + 1) % n,
    ArrowLeft:  (curr - 1 + n) % n,
    Home: 0,
    End:  n - 1,
  }
  if (!(e.key in nextMap)) return
  e.preventDefault()
  kbIdx.value = nextMap[e.key]
  measureAt(kbIdx.value)
  navEl.value?.querySelectorAll('[role="tab"]')[kbIdx.value]?.focus()
}

// ── Scroll & resize ───────────────────────────────────────────────────────────
const onScroll = () => isSticky.value = scrollY > 60
const checkMobile = () => { isMobile.value = window.innerWidth <= 991 }

onMounted(async () => {
  checkMobile()
  window.addEventListener('scroll', onScroll, { passive: true })
  window.addEventListener('resize', checkMobile, { passive: true })
  await nextTick()
  measureFull()
  await nextTick()
  requestAnimationFrame(() => ready.value = true)
  new ResizeObserver(() => measureFull()).observe(containerEl.value)
})

onUnmounted(() => {
  window.removeEventListener('scroll', onScroll)
  window.removeEventListener('resize', checkMobile)
})
</script>

<style scoped>
.nav-slide {
  opacity: 1;
  transition: transform 0.38s cubic-bezier(0.34, 1.4, 0.64, 1), width 0.38s cubic-bezier(0.34, 1.4, 0.64, 1), height 0.35s cubic-bezier(0.34, 1.4, 0.64, 1), border-radius 0.25s ease;
}
.nav-tab:focus-visible {
  box-shadow: 0 0 0 2px #44C486;
}
</style>
