<template>
  <f7-page>
    <f7-navbar title="Dialog" back-link="Back"></f7-navbar>
    <div class="block block-strong">
      <p>There are 1:1 replacements of native Alert, Prompt and Confirm modals. They support callbacks, have very easy api and can be combined with each other. Check these examples:</p>
      <p class="row">
        <button class="col button button-raised" @click="openAlert">Alert</button>
        <button class="col button button-raised" @click="openConfirm">Confirm</button>
        <button class="col button button-raised" @click="openPrompt">Prompt</button>
      </p>
      <p class="row">
        <button class="col button button-raised" @click="openLogin">Login</button>
        <button class="col button button-raised" @click="openPassword">Password</button>
      </p>
    </div>
    <f7-block-title>Vertical Buttons</f7-block-title>
    <div class="block block-strong">
      <p>
        <button class="button button-raised" @click="openVerticalButtons">Vertical Buttons</button>
      </p>
    </div>
    <f7-block-title>Preloader Dialog</f7-block-title>
    <div class="block block-strong">
      <p class="row">
        <button class="col button button-raised" @click="openPreloader">Preloader</button>
        <button class="col button button-raised" @click="openCustomPreloader">Custom Text</button>
      </p>
    </div>
    <f7-block-title>Progress Dialog</f7-block-title>
    <div class="block block-strong">
      <p class="row">
        <button class="col button button-raised" @click="openInfiniteProgress">Infinite</button>
        <button class="col button button-raised" @click="openDeterminedProgress">Determined</button>
      </p>
    </div>
    <f7-block-title>Dialogs Stack</f7-block-title>
    <div class="block block-strong">
      <p>This feature doesn't allow to open multiple dialogs at the same time, and will automatically open next dialog when you close the current one. Such behavior is similar to browser native dialogs: </p>
      <p>
        <button class="button button-raised" @click="openAlerts">Open Multiple Alerts</button>
      </p>
    </div>
  </f7-page>
</template>
<script>
  import { f7Navbar, f7Page, f7BlockTitle } from 'framework7-vue';

  export default {
    components: {
      f7Navbar,
      f7Page,
      f7BlockTitle,
    },
    methods: {
      openAlert: function () {
        var app = this.$f7;
        app.dialog.alert('Hello!');
      },
      openConfirm: function () {
        var app = this.$f7;
        app.dialog.confirm('Are you feel good today?', function () {
          app.dialog.alert('Great!');
        });
      },
      openPrompt: function () {
        var app = this.$f7;
        app.dialog.prompt('What is your name?', function (name) {
          app.dialog.confirm('Are you sure that your name is ' + name + '?', function () {
            app.dialog.alert('Ok, your name is ' + name);
          });
        });
      },
      openLogin: function () {
        var app = this.$f7;
        app.dialog.login('Enter your username and password', function (username, password) {
          app.dialog.alert('Thank you!<br>Username:' + username + '<br>Password:' + password);
        });
      },
      openPassword: function () {
        var app = this.$f7;
        app.dialog.password('Enter your username and password', function (password) {
          app.dialog.alert('Thank you!<br>Password:' + password);
        });
      },
      openAlerts: function () {
        var app = this.$f7;
        app.dialog.alert('Alert 1');
        app.dialog.alert('Alert 2');
        app.dialog.alert('Alert 3');
        app.dialog.alert('Alert 4');
        app.dialog.alert('Alert 5');
      },
      openVerticalButtons: function () {
        var app = this.$f7;
        app.dialog.create({
          title: 'Vertical Buttons',
          buttons: [
            {
              text: 'Button 1',
            },
            {
              text: 'Button 2',
            },
            {
              text: 'Button 3',
            },
          ],
          verticalButtons: true,
        }).open();
      },
      openPreloader: function () {
        var app = this.$f7;
        app.dialog.preloader();
        setTimeout(function () {
          app.dialog.close();
        }, 3000);
      },
      openCustomPreloader: function () {
        var app = this.$f7;
        app.dialog.preloader('My text...');
        setTimeout(function () {
          app.dialog.close();
        }, 3000);
      },
      openInfiniteProgress: function () {
        var app = this.$f7;
        app.dialog.progress();
        setTimeout(function () {
          app.dialog.close();
        }, 3000);
      },
      openDeterminedProgress: function () {
        var app = this.$f7;
        var progress = 0;
        var dialog = app.dialog.progress('Loading assets', progress);
        dialog.setText('Image 1 of 10');
        var interval = setInterval(function () {
          progress += 10;
          dialog.setProgress(progress);
          dialog.setText('Image ' + ((progress) / 10) + ' of 10');
          if (progress === 100) {
            clearInterval(interval);
            dialog.close();
          }
        }, 300)
      },
    }
  }
</script>
