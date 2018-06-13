Vue.component('navbar-component', {
  props: ['tagline'],
  template: '<nav class="navbar navbar-toggleable-md fixed-top navbar-inverse bg-inverse">' +
                '<a class="navbar-brand" href="index.html">' +
                  '<img src="assets/img/MKTURBO_PinkLogo150x30.png" class="d-inline-block align-top" alt="MKTurbo Logo"/>' +
                  '<span class="hidden-xs-down"> {{tagline}}</span>' +
                '</a>' +
             '</nav>',
})


Vue.component('sidebar-offcanvas', {
props: ['nav'],
  template:'<div class="list-group">' +
      '<a v-for="item in nav" class="list-group-item border-0 list-group-item-action rounded my-1" :href="item.url">{{item.link}}</a>' +
    '</div>',
})

Vue.component('footer-component', {
props: ['year'],
  template: '<footer><hr /><p class="mt-5">&copy; Copyright 2017-{{year}} MK Turbo. All Rights Reserved.</p></footer>',
})


var app = new Vue({
  el: '#app',
  data: function() {
  return {
    tagline: 'Make your miata go from Meow to RAWR!',
    navigation: [
      {link: '90-93 NA6 Turbo kit', url: '9093NA6.html'},
      {link: '90-97 NA8 Turbo kit', url: '9097NA8.html'},
      {link: '99-05 NB1/NB2 Turbo kit', url: '9905NB.html'},
      {link: 'Oil Line Kit', url: 'oilline.html'},
      {link: 'Reviews', url: 'reviews.html'},
      {link: 'FAQs', url: 'faq.html'},
      {link: 'Dynos', url: 'dynos.html'},
      {link: 'Installation & Instructions', url: 'installation.html'},
      {link: 'About MKTurbo', url: 'aboutMKT.html'},
    ],
    year: [],
		};
	},

  created: function() {
   this.fetchData();
  },

  methods: {
   fetchData: function() {
      var d = new Date();
      this.year = d.getFullYear();
   }
  },
})
