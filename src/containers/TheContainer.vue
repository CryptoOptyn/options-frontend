<template>
  <div class="c-app">
    <TheSidebar/>
    <CWrapper>
      <TheHeader/>
      <div class="c-body">
        <main class="c-main">
          <CContainer fluid>
            <transition name="fade" mode="out-in">
              <router-view :key="$route.path"></router-view>
            </transition>
          </CContainer>
        </main>
         <b-modal id="modal-center" centered title="Network not supported" v-model="networkIsNotSupported"  ok-only>
            <p class="my-4">
            This network currently isn't supported. Please change to a supported network and refresh the page.<br><br>
            Mainnets: Polygon<br><br>
            Testnets: Rinkeby, Binance Smart Chain, Polygon, Moonbeam<br>
            </p>
        </b-modal>
         <b-modal id="modal-center" centered title="Warning" v-model="networkIsSupported"  ok-only ok-title="I understand" >
            <p class="my-4">
            Optyn is unaudited beta smart contract software. <br>Only use funds that you can afford to lose.<br><br>
            </p>
        </b-modal>

      </div>
      <TheFooter/>
    </CWrapper>
  </div>
</template>

<script>
import { store } from "../api/Store";
import TheSidebar from './TheSidebar'
import TheHeader from './TheHeader'
import TheFooter from './TheFooter'

export default {
  name: 'TheContainer',
  data() {
      return {
        networkIsSupported: false,
        networkIsNotSupported: false,
      }
  },
  components: {
    TheSidebar,
    TheHeader,
    TheFooter
  },
   mounted() {
     console.log("networkIsSupported:",store.networkIsSupported);
     if (store.networkIsSupported){
       this.networkIsSupported = true;
       this.networkIsNotSupported = false;
     }
     else{
       this.networkIsSupported = false;
       this.networkIsNotSupported = true;
     }
   }
}
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
