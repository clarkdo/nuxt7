<template>
  <f7-page>
    <f7-navbar title="Photo Browser" back-link="Back"></f7-navbar>
    <div class="block">
      <p>Photo Browser is a standalone and highly configurable component that allows to open window with photo viewer and navigation elements with the following features:</p>
      <ul>
        <li>Swiper between photos</li>
        <li>Multi-gestures support for zooming</li>
        <li>Toggle zoom by double tap on photo</li>
        <li>Single click on photo to toggle Exposition mode</li>
      </ul>
    </div>
    <div class="block">
      <p>Photo Browser could be opened in a three ways - as a Standalone component (Popup modification), in Popup, and as separate Page:</p>
      <div class="row">
        <div class="col-33"><a href="#" class="button button-raised" @click="openStandalone">Standalone</a></div>
        <div class="col-33"><a href="#" class="button button-raised" @click="openPopup">Popup</a></div>
        <div class="col-33"><a href="#" class="button button-raised" @click="openPage">Page</a></div>
      </div>
    </div>
    <div class="block">
      <p>Photo Browser suppots 2 default themes - default Light (like in previous examples) and Dark theme. Here is a Dark theme examples:</p>
      <div class="row">
        <div class="col-33"><a href="#" class="button button-raised" @click="openStandaloneDark">Standalone</a></div>
        <div class="col-33"><a href="#" class="button button-raised" @click="openPopupDark">Popup</a></div>
        <div class="col-33"><a href="#" class="button button-raised" @click="openPageDark">Page</a></div>
      </div>
    </div>
  </f7-page>
</template>
<script>
  import { f7Navbar, f7Page } from 'framework7-vue';

  export default {
    data: function () {
      return {
        photos: [
          {
            url: 'img/beach.jpg',
            caption: 'Amazing beach in Goa, India'
          },
          'http://placekitten.com/1024/1024',
          'img/lock.jpg',
          {
            url: 'img/monkey.jpg',
            caption: 'I met this monkey in Chinese mountains'
          },
          {
            url: 'img/mountains.jpg',
            caption: 'Beautiful mountains in Zhangjiajie, China'
          }
        ],
      }
    },
    methods: {
      openStandalone: function () {
        const self = this;
        self.standalone.open();
      },
      openPopup: function () {
        const self = this;
        self.popup.open();
      },
      openPage: function () {
        const self = this;
        self.page.open();
      },
      openStandaloneDark: function () {
        const self = this;
        self.standaloneDark.open();
      },
      openPopupDark: function () {
        const self = this;
        self.popupDark.open();
      },
      openPageDark: function () {
        const self = this;
        self.pageDark.open();
      },
    },
    on: {
      pageInit: function () {
        const self = this;
        // Create PBs when page init
        self.standalone = self.$f7.photoBrowser.create({
          photos: self.photos,
        });
        self.popup = self.$f7.photoBrowser.create({
          photos: self.photos,
          type: 'popup',
        });
        self.page = self.$f7.photoBrowser.create({
          photos: self.photos,
          type: 'page',
          backLinkText: 'Back',
        });
        self.standaloneDark = self.$f7.photoBrowser.create({
          photos: self.photos,
          theme: 'dark',
        });
        self.popupDark = self.$f7.photoBrowser.create({
          photos: self.photos,
          type: 'popup',
          theme: 'dark',
        });
        self.pageDark = self.$f7.photoBrowser.create({
          photos: self.photos,
          type: 'page',
          backLinkText: 'Back',
          theme: 'dark',
        });
      },
      pageBeforeRemove: function () {
        const self = this;
        // Destroy PBs on page remove
        self.standalone.destroy();
        self.popup.destroy();
        self.page.destroy();
        self.standaloneDark.destroy();
        self.popupDark.destroy();
        self.pageDark.destroy();
      },
    }
  };
</script>
