
  <template>
    <transition name="fade">
      <div class="slide-content-wrapper" v-show="menuVisible && settingVisible === 3">
        <transition name="slide-right">
          <div class="content" v-if="settingVisible === 3 " >
            <div class="content-page-wrapper" v-if="bookAvailable" >
              <div class="content-page">
                <keep-alive>
                  <component :is="tab === 1 ? content : content"></component>
                </keep-alive>
              </div>
              <div class="content-page-tab">
                <div class="content-page-tab-item"
                     :class="{'selected': tab === 1}"
                     @click="selectTab(1)">{{$t('book.navigation')}}
                </div>
              </div>
            </div>
            <div class="empty" v-else >
              <ebook-loading></ebook-loading>
            </div>
          </div>
        </transition>
        <div class="content-bg" v-if="settingVisible === 3 || settingVisible === 4" @click="hideTitleAndMenu()"></div>
      </div>
    </transition>
  </template>
<script>
import { ebookMixin } from '@/utils/mixin'
import EbookSlideContents from '@/components/ebook/EbookSlideContents'
import EbookLoading from '@/components/ebook/EbookLoading'
export default {
  name: 'EbookSlide',
  mixins: [ebookMixin],
  data () {
    return {
      tab: 1,
      content: EbookSlideContents
    }
  },
  components: {
    EbookSlideContents,
    EbookLoading
  },
  methods: {
    selectTab (tab) {
      this.tab = tab
    }
  }
}
</script>

<style lang="scss" scoped>
@import "../../assets/styles/global";

.slide-content-wrapper {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 350;
  display: flex;
  width: 100%;
  height: 100%;
  .content {
    flex: 0 0 85%;
    width: 85%;
    height: 100%;
    .content-page-wrapper {
      display: flex;
      flex-direction: column;
      width: 100%;
      height: 100%;
      .content-page {
        flex: 1;
        width: 100%;
        overflow: hidden;
      }
      .content-page-tab {
        display: flex;
        flex: 0 0 px2rem(48);
        .content-page-tab-item {
          flex: 1;
          font-size: px2rem(12);
          @include center;
        }
      }
    }
    .empty {
      width: 100%;
      height: 100%;
      @include center;
      font-size: px2rem(16);
      color: #333;
    }
  }
  .content-bg {
    flex: 0 0 15%;
    width: 15%;
    height: 100%;
  }
}
</style>
