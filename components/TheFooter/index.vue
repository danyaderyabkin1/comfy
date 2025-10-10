<script setup lang="ts">
const cookie = useCookie('noty')
const cookieMain = useCookie('cook')
const acceptCookie = () => cookie.value = '1'
const acceptCookieMain = () => cookieMain.value = '1'
</script>


<template>
  <footer class="footer">
    <div class="container footer__container">
      <div class="footer__wrap">
        <NuxtLink to="/">
          <img src="/assets/images/logo-1.webp" alt="logo">
<!--          <span class="font-semibold">С Вами в любой точке страны</span>-->
        </NuxtLink>
        <div>
          <div class="footer__info">
            <p class="font-semibold mb-2">
              Ивановская область,
              г. Родники, ул. Трудовая, д. 16
            </p>
            <p class="footer__phone">
              <a href="tel:+79158251758">+7 915 825 17 58</a>
            </p>
            <p class="footer__phone-medium">
              <a href="tel:+79115119990">+7 911 511-99-90</a>
            </p>
            <p class="footer__mail">
              <a href="mailto:info@comfy-meb.ru">info@comfy-meb.ru</a>
            </p>
            <p class="font-semibold text-lg">
              написать нам
            </p>
          </div>
          <div class="footer__contacts">
            <a
                href="https://api.whatsapp.com/send/?phone=%2B79621690551&text&type=phone_number&app_absent=0"
                target="_blank">
              <UIcon name="i-mingcute-whatsapp-fill" class="size-10 text-[#25d366]"/>
            </a>
            <a href="https://t.me/+79621690551" target="_blank">
              <UIcon name="uil:telegram" class="size-10 text-[#2ca5e0]"/>
            </a>
          </div>

        </div>
      </div>
      <nav class="nav">
        <div class="nav__wrap">
          <h3>Каталог</h3>
          <div class="nav__double">
              <TheFooterSubMenu/>
          </div>
        </div>
        <div class="nav__wrap">
          <h3>Comfy</h3>
          <ul class="nav__list">
            <li class="nav__item">
              <NuxtLink class="nav__link" to="/aboutus#about">Вступление</NuxtLink>
            </li>
<!--            <li class="nav__item">-->
<!--              <NuxtLink class="nav__link" to="/aboutus#sert">Сертификаты</NuxtLink>-->
<!--            </li>-->
<!--            <li class="nav__item">-->
<!--              <NuxtLink class="nav__link" to="/aboutus#thank">Благодарности</NuxtLink>-->
<!--            </li>-->
            <li class="nav__item">
              <NuxtLink class="nav__link" to="/aboutus#pay">Оплата и доствка</NuxtLink>
            </li>
            <li class="nav__item">
              <NuxtLink class="nav__link" to="/contacts">Контактная информация</NuxtLink>
            </li>
<!--            <li class="nav__item">-->
<!--              <NuxtLink class="nav__link" to="/aboutus#contacts">Обратная связь</NuxtLink>-->
<!--            </li>-->
            <li class="nav__item">
              <NuxtLink class="nav__link" to="/politika">Персональные данные</NuxtLink>
            </li>
            <li class="hidden xl:flex justify-end mt-auto w-full">
              <a href="https://moovix.ru/" target="_blank" rel="noopener noreferrer">
                <img src="/assets/images/moovix.png" alt="moovix">
              </a>
            </li>
          </ul>
        </div>
        <!--        <div class="nav__wrap">-->
        <!--          <h3>Информация</h3>-->
        <!--          <ul class="nav__list">-->
        <!--            <li class="nav__item">-->
        <!--              <NuxtLink class="nav__link" to="/politika">Политика конфиденциальности</NuxtLink>-->
        <!--            </li>-->
        <!--            <li class="nav__item">-->
        <!--              <NuxtLink class="nav__link" to="/politika">Обработка персональных данных</NuxtLink>-->
        <!--            </li>-->
        <!--          </ul>-->
        <!--        </div>-->
      </nav>
      <div class="text-center block xl:hidden mt-10">
        <p>© 2017-{{ new Date().getFullYear() }} Comfy-Meb | Все права защищены</p>
        <a class="flex justify-center mt-2" href="https://moovix.ru/" target="_blank" rel="noopener noreferrer">
          <img class="w-14 lg:w-fit" src="/assets/images/moovix.png" alt="moovix">
        </a>
      </div>

    </div>
    <div v-if="!cookie" id="cookie_note" class="show"><p>Наши цены напрямую зависят от курса доллара. В связи с этим,
      актуальные цены
      следует уточнять у наших менеджеров. Мы всегда готовы предоставить вам наиболее актуальную информацию о стоимости
      наших товаров и услуг. Спасибо за понимание и сотрудничество!.</p>
      <p>
        <button class="cookie_accept btn btn-primary" @click.prevent="acceptCookie">Принять</button>
      </p>
    </div>
    <div v-if="!cookieMain" id="cookie_note"  class="show btm">
      <p>
        Мы используем файлы <router-link class="underline" to="/politika">cookie.</router-link> Продолжая работу Вы принимаете условия пользования
      </p>
      <p>
        <button class="cookie_accept btn btn-primary" @click.prevent="acceptCookieMain">Согласен</button>
      </p>
    </div>
    <ul class="bottom-menu">
      <li>
        <RouterLink to="/krovati">
          <img src="/assets/images/description/weave.svg" alt="">
          <span>Текстиль</span>
        </RouterLink>
      </li>
      <li>
        <RouterLink to="/mebel">
          <img src="/assets/images/furniture-bed-svgrepo-com%201.svg" alt="">
          <span>Мебель</span>
        </RouterLink>
      </li>
      <li>
        <RouterLink to="/">
          <img src="/assets/images/hm.svg" alt="">
          <span>Главная</span>
        </RouterLink>
      </li>
      <li>
        <RouterLink to="/aboutus">
          <img src="/assets/images/about-description-help-svgrepo-com%201.svg" alt="">
          <span>О компании</span>
        </RouterLink>
      </li>
      <li>
        <RouterLink to="/aboutus#contacts">
          <img src="/assets/images/SVGRepo_ic.svg" alt="">
          <span>Контакты</span>
        </RouterLink>
      </li>
    </ul>
  </footer>
  <div class="socials-right shadow-md">
    <a href="https://vk.com/comfy.meb37" target="_blank">
      <svg width="32" height="32" viewBox="0 0 32 32" fill="none" xmlns="http://www.w3.org/2000/svg">
        <g clip-path="url(#clip0_2_734)">
          <path d="M11.3426 0.792084H20.6733C29.1961 0.792084 31.208 2.81981 31.208 11.3426V20.6733C31.208 29.196 29.1802 31.2079 20.6575 31.2079H11.3268C2.804 31.2079 0.792114 29.1802 0.792114 20.6574V11.3267C0.792114 2.81981 2.81984 0.792084 11.3426 0.792084Z" fill="#5181B8"/>
          <mask id="mask0_2_734" style="mask-type:luminance" maskUnits="userSpaceOnUse" x="0" y="0" width="32" height="32">
            <path d="M11.3426 0.792084H20.6733C29.1961 0.792084 31.208 2.81981 31.208 11.3426V20.6733C31.208 29.196 29.1802 31.2079 20.6575 31.2079H11.3268C2.804 31.2079 0.792114 29.1802 0.792114 20.6574V11.3267C0.792114 2.81981 2.81984 0.792084 11.3426 0.792084Z" fill="white"/>
          </mask>
          <g mask="url(#mask0_2_734)">
            <path d="M0 0H32V32H0V0Z" fill="#5181B8"/>
          </g>
          <path fill-rule="evenodd" clip-rule="evenodd" d="M25.695 11.2634C25.8376 10.7881 25.695 10.4554 25.0297 10.4554H22.8119C22.2416 10.4554 21.9881 10.7564 21.8455 11.0891C21.8455 11.0891 20.7208 13.8455 19.1208 15.6198C18.598 16.1426 18.3762 16.301 18.0911 16.301C17.9485 16.301 17.7426 16.1426 17.7426 15.6673V11.2634C17.7426 10.6931 17.5842 10.4554 17.1089 10.4554H13.6238C13.2752 10.4554 13.0535 10.7248 13.0535 10.9624C13.0535 11.501 13.8455 11.6277 13.9406 13.1168V16.3802C13.9406 17.0931 13.8139 17.2198 13.5287 17.2198C12.7842 17.2198 10.9465 14.4634 9.8693 11.295C9.64752 10.7089 9.44158 10.4554 8.87128 10.4554H6.65346C6.0198 10.4554 5.89307 10.7564 5.89307 11.0891C5.89307 11.6752 6.63762 14.5901 9.39406 18.4396C11.2317 21.0693 13.8139 22.495 16.1584 22.495C17.5683 22.495 17.7426 22.1782 17.7426 21.6396V19.6436C17.7426 19.0099 17.8693 18.8832 18.3287 18.8832C18.6614 18.8832 19.2158 19.0416 20.5307 20.3089C22.0356 21.8139 22.2891 22.495 23.1287 22.495H25.3465C25.9802 22.495 26.297 22.1782 26.1069 21.5604C25.901 20.9426 25.1881 20.0396 24.2376 18.9624C23.7148 18.3446 22.9386 17.695 22.7168 17.3624C22.3842 16.9347 22.4792 16.7446 22.7168 16.3802C22.7168 16.3644 25.4257 12.5624 25.695 11.2634Z" fill="white"/>
        </g>
        <defs>
          <clipPath id="clip0_2_734">
            <rect width="32" height="32" fill="white"/>
          </clipPath>
        </defs>
      </svg>
    </a>
<!--    <a href="https://yandex.ru/maps/-/CLFqa6k9" target="_blank">-->
<!--      <svg width="32" height="32" viewBox="0 0 32 32" fill="none" xmlns="http://www.w3.org/2000/svg">-->
<!--        <g clip-path="url(#clip0_2_745)">-->
<!--          <path d="M14.2667 32V21.6187L7.33337 3.00001H10.8214L15.9334 17.356L21.8134 -0.00132751H25.02L17.476 21.736V31.9987L14.2667 32Z" fill="#E24642"/>-->
<!--        </g>-->
<!--        <defs>-->
<!--          <clipPath id="clip0_2_745">-->
<!--            <rect width="32" height="32" fill="white"/>-->
<!--          </clipPath>-->
<!--        </defs>-->
<!--      </svg>-->
<!--    </a>-->
    <a href="https://www.ozon.ru/brand/comfy-meb-100098308/?__rr=1" target="_blank">
      <img class="w-8 h-8  rounded-full" src="/public/assets/images/about/c4e9bf55d8134a9f8e0a78968a5fb896747ea0d4.png" alt="ozon">
    </a>
    <a href="https://www.wildberries.ru/brands/comfy-meb" target="_blank">
      <img class="w-8 h-8  rounded-full" src="/public/assets/images/about/2420fad29c780fcb5f42588d671df7c8da6ead15.png" alt="wb">
    </a>
    <a href="https://market.yandex.ru/business--comfy-meb/41471413" target="_blank">
      <img class="w-8 h-8  rounded-full" src="/public/assets/images/about/b11d28bb16248ea516aa407ee955807d1f67e558.png" alt="market">
    </a>
    <a href="https://megamarket.ru/catalog/?q=comfy-meb&suggestionType=constructor" target="_blank">
      <img class="w-8 h-8 rounded-full" src="/public/assets/images/about/1ddc6ce957049ccc5ac3c871f64fee742954df2d.png" alt="">
    </a>
  </div>
  <Teleport to="body">
<!--    <TheFooterCart/>-->
  </Teleport>
</template>

<style scoped>
.socials-right {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  position: fixed;
  right: 0;
  top: 30%;
  background-color: #fff;
  padding: 15px 5px 15px 15px;
  z-index: 99;
  border-radius: 30px 0 0 30px;
}

#cookie_note {
  display: flex;
  z-index: 99;
  position: fixed;
  bottom: 15px;
  left: 2%;
  max-width: 475px;
  padding: 20px;
  background-color: white;
  border-radius: 4px;
  box-shadow: 2px 3px 10px rgba(0, 0, 0, 0.2);
  font-size: 12px;
}

#cookie_note.btm {
  bottom: 170px;
}

.cookie_accept {
  width: auto;
  cursor: pointer;
  white-space: nowrap;
  padding: 10px 20px;
  border: navajowhite;
  background-color: #2b70fa;
  color: #fff;
  margin-left: 20px;
  border-radius: 5px;
  font-size: 10px;
}

@media (max-width: 767.98px) {
  #cookie_note {
    flex-direction: column;
    max-width: 96%;
  }
  #cookie_note.btm {
    bottom: 200px;
  }

  .cookie_accept {
    margin-left: 0;
    margin-top: 10px;
    width: 100%;
  }
}
</style>