<template>
  <f7-page>
    <f7-navbar title="Pull To Refresh" back-link="Back"></f7-navbar>
    <div data-infinite-distance="50" class="page-content ptr-content" @ptr:refresh="loadMore">
      <div class="ptr-preloader">
        <div class="preloader"></div>
        <div class="ptr-arrow"></div>
      </div>
      <div class="list media-list">
        <ul>
          <li class="item-content">
            <div class="item-media"><img src="http://lorempixel.com/88/88/abstract/1" width="44"/></div>
            <div class="item-inner">
              <div class="item-title-row">
                <div class="item-title">Yellow Submarine</div>
              </div>
              <div class="item-subtitle">Beatles</div>
            </div>
          </li>
          <li class="item-content">
            <div class="item-media"><img src="http://lorempixel.com/88/88/abstract/2" width="44"/></div>
            <div class="item-inner">
              <div class="item-title-row">
                <div class="item-title">Don't Stop Me Now</div>
              </div>
              <div class="item-subtitle">Queen</div>
            </div>
          </li>
          <li class="item-content">
            <div class="item-media"><img src="http://lorempixel.com/88/88/abstract/3" width="44"/></div>
            <div class="item-inner">
              <div class="item-title-row">
                <div class="item-title">Billie Jean</div>
              </div>
              <div class="item-subtitle">Michael Jackson</div>
            </div>
          </li>
        </ul>
        <div class="block-footer">
          <p>Just pull page down to let the magic happen.<br>Note that pull-to-refresh feature is optimised for touch and native scrolling so it may not work on desktop browser.</p>
        </div>
      </div>
    </div>
  </f7-page>
</template>
<script>
  import { f7Navbar, f7Page } from 'framework7-vue';

  export default {
    data: function () {
      return {
        songs: ['Yellow Submarine', 'Don\'t Stop Me Now', 'Billie Jean', 'Californication'],
        authors: ['Beatles', 'Queen', 'Michael Jackson', 'Red Hot Chili Peppers']
      }
    },
    methods: {
      loadMore: function (e, done) {
        var self = this;
        var $ = self.$$;

        setTimeout(function () {
          var picURL = 'http://lorempixel.com/88/88/abstract/' + Math.round(Math.random() * 10);
          var song = self.songs[Math.floor(Math.random() * self.songs.length)];
          var author = self.authors[Math.floor(Math.random() * self.authors.length)];

          var linkHTML =
          '<li class="item-content">' +
            '<div class="item-media"><img src="' + picURL + '" width="44"/></div>' +
            '<div class="item-inner">' +
              '<div class="item-title-row">' +
                '<div class="item-title">' + song + '</div>' +
              '</div>' +
              '<div class="item-subtitle">' + author + '</div>' +
            '</div>' +
          '</li>';

          $(self.$el).find('.list ul').append(linkHTML);

          done();

        }, 1000);
      }
    }
  }
</script>
