<script setup lang="ts">
const linkCols = [
  { title: 'PRODUCTS 🔥', items: ['HR Management', 'Invoice System', 'Email Marketing', 'Web Services', 'Digital Marketing'] },
  { title: 'WHY CHOOSE 🌟', items: ['Customers', 'Why Staco ?', 'Book a demo'] },
  { title: 'RESOURCES ❇️', items: ['Latest Blog', 'Supports', 'Knowledgebase', 'FAQs'] },
  { title: 'COMPANY 💎', items: ['About', 'What we do', 'Contact us', 'Careers'] },
]

const legalLinks = ['Terms and conditions', 'Cookies', 'Privacy policy']
</script>

<template>
  <div class="bg-[#ecf1f1] px-[30px] pb-[30px] max-w-[1560px] mx-auto relative z-[2]">
    <footer class="bg-[#1f2334] rounded-[30px] overflow-hidden">

      <!-- Top -->
      <div class="pt-[100px] pb-[70px]">
        <div class="max-w-[1320px] mx-auto px-[60px] max-[991px]:px-[30px]">
          <div class="grid grid-cols-[320px_1fr] gap-[60px] max-[991px]:grid-cols-1 max-[991px]:gap-10">

            <!-- Brand -->
            <div>
              <a href="#" class="flex items-center gap-3 mb-5 no-underline">
              <img src="~/assets/images/icons/logo.svg" alt="logo"></a>
              <p class="text-sm font-medium leading-7 text-white/45 mb-7">
                Staco is the dedicated platform for performance management that helps to grow your startup quickly
              </p>
              <!-- Socials -->
              <ul class="flex gap-2.5 list-none p-0 m-0">
                <li>
                  <a href="#" aria-label="Facebook" class="social-link">
                    <span class="si-wrap">
                      <span class="si-slot"><svg viewBox="0 0 24 24" fill="currentColor" class="w-4 h-4"><path d="M18 2h-3a5 5 0 00-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 011-1h3z"/></svg></span>
                      <span class="si-slot"><svg viewBox="0 0 24 24" fill="currentColor" class="w-4 h-4"><path d="M18 2h-3a5 5 0 00-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 011-1h3z"/></svg></span>
                    </span>
                  </a>
                </li>
                <li>
                  <a href="#" aria-label="Twitter" class="social-link">
                    <span class="si-wrap">
                      <span class="si-slot"><svg viewBox="0 0 24 24" fill="currentColor" class="w-4 h-4"><path d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z"/></svg></span>
                      <span class="si-slot"><svg viewBox="0 0 24 24" fill="currentColor" class="w-4 h-4"><path d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z"/></svg></span>
                    </span>
                  </a>
                </li>
                <li>
                  <a href="#" aria-label="LinkedIn" class="social-link">
                    <span class="si-wrap">
                      <span class="si-slot"><svg viewBox="0 0 24 24" fill="currentColor" class="w-4 h-4"><path d="M16 8a6 6 0 016 6v7h-4v-7a2 2 0 00-2-2 2 2 0 00-2 2v7h-4v-7a6 6 0 016-6zM2 9h4v12H2z"/><circle cx="4" cy="4" r="2"/></svg></span>
                      <span class="si-slot"><svg viewBox="0 0 24 24" fill="currentColor" class="w-4 h-4"><path d="M16 8a6 6 0 016 6v7h-4v-7a2 2 0 00-2-2 2 2 0 00-2 2v7h-4v-7a6 6 0 016-6zM2 9h4v12H2z"/><circle cx="4" cy="4" r="2"/></svg></span>
                    </span>
                  </a>
                </li>
                <li>
                  <a href="#" aria-label="Instagram" class="social-link">
                    <span class="si-wrap">
                      <span class="si-slot"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" class="w-4 h-4"><rect x="2" y="2" width="20" height="20" rx="5"/><circle cx="12" cy="12" r="4"/><circle cx="17.5" cy="6.5" r="1" fill="currentColor" stroke="none"/></svg></span>
                      <span class="si-slot"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" class="w-4 h-4"><rect x="2" y="2" width="20" height="20" rx="5"/><circle cx="12" cy="12" r="4"/><circle cx="17.5" cy="6.5" r="1" fill="currentColor" stroke="none"/></svg></span>
                    </span>
                  </a>
                </li>
                <li>
                  <a href="#" aria-label="YouTube" class="social-link">
                    <span class="si-wrap">
                      <span class="si-slot"><svg viewBox="0 0 24 24" fill="currentColor" class="w-4 h-4"><path d="M22.54 6.42a2.78 2.78 0 00-1.95-1.96C18.88 4 12 4 12 4s-6.88 0-8.59.46A2.78 2.78 0 001.46 6.42 29 29 0 001 12a29 29 0 00.46 5.58 2.78 2.78 0 001.95 1.96C5.12 20 12 20 12 20s6.88 0 8.59-.46a2.78 2.78 0 001.95-1.96A29 29 0 0023 12a29 29 0 00-.46-5.58z"/><polygon points="9.75 15.02 15.5 12 9.75 8.98 9.75 15.02" fill="#1f2334"/></svg></span>
                      <span class="si-slot"><svg viewBox="0 0 24 24" fill="currentColor" class="w-4 h-4"><path d="M22.54 6.42a2.78 2.78 0 00-1.95-1.96C18.88 4 12 4 12 4s-6.88 0-8.59.46A2.78 2.78 0 001.46 6.42 29 29 0 001 12a29 29 0 00.46 5.58 2.78 2.78 0 001.95 1.96C5.12 20 12 20 12 20s6.88 0 8.59-.46a2.78 2.78 0 001.95-1.96A29 29 0 0023 12a29 29 0 00-.46-5.58z"/><polygon points="9.75 15.02 15.5 12 9.75 8.98 9.75 15.02" fill="#1f2334"/></svg></span>
                    </span>
                  </a>
                </li>
              </ul>
            </div>

            <!-- Link columns -->
            <div class="grid grid-cols-4 gap-[30px] max-[767px]:grid-cols-2">
              <div v-for="col in linkCols" :key="col.title">
                <h6 class="text-[13px] font-bold text-white mb-[22px] tracking-[0.02em]">{{ col.title }}</h6>
                <ul class="flex flex-col gap-3 list-none p-0 m-0">
                  <li v-for="item in col.items" :key="item">
                    <a href="#" class="widget-link">{{ item }}</a>
                  </li>
                </ul>
              </div>
            </div>

          </div>
        </div>
      </div>

      <!-- Bottom bar -->
      <div class="border-t border-white/[0.08] py-[22px]">
        <div class="max-w-[1320px] mx-auto px-[60px] max-[991px]:px-[30px]">
          <div class="flex items-center justify-between gap-5 flex-wrap">
            <p class="text-sm text-white/30">
              2023 <a href="#" class="text-white/50 no-underline transition-colors duration-200 hover:text-[#B2EDA1]">Staco</a>. All rights reserved.
            </p>
            <ul class="flex gap-7 list-none p-0 m-0">
              <li v-for="link in legalLinks" :key="link">
                <a href="#" class="footer-link">
                  <span class="widget-normal">{{ link }}</span>
                  <span class="widget-hover">{{ link }}</span>
                </a>
              </li>
            </ul>
          </div>
        </div>
      </div>

    </footer>
  </div>
</template>

<style scoped>
.social-link {
  width: 38px;
  height: 38px;
  border-radius: 50%;
  border: 2px solid rgba(255, 255, 255, 0.15);
  display: flex;
  align-items: flex-start;
  justify-content: center;
  color: white;
  text-decoration: none;
  overflow: hidden;
  transition: border 0.3s, background 0.3s;
}
.social-link:hover {
  border: 2px solid rgba(255, 255, 255, 0.2);
  background: rgba(255, 255, 255, 0.15);
}
.si-wrap {
  display: flex;
  flex-direction: column;
  transition: transform 0.3s cubic-bezier(.15,.85,.31,1);
}
.si-slot {
  width: 38px;
  height: 38px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}
.social-link:hover .si-wrap {
  transform: translateY(-38px);
}

.widget-link {
  color: rgba(255, 255, 255, 0.698);
  font-size: 16px;
  font-weight: 500;
  line-height: 1.5;
  text-decoration: none;
  transition: color 0.3s;
}
.widget-link:hover {
  color: rgb(255, 255, 255);
}

.footer-link {
  color: rgba(255, 255, 255, 0.3);
  font-size: 14px;
  font-weight: 500;
  text-decoration: none;
  display: inline-block;
  overflow: hidden;
  position: relative;
}
.footer-link:hover .widget-normal { transform: translateY(-150%); opacity: 0; }
.footer-link:hover .widget-hover { transform: translateY(-50%); opacity: 1; color: #B2EDA1; }
</style>
