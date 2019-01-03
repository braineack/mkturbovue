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
props: ['nav', 'url'],
  template:'<div class="list-group">' +
      '<a v-for="item in nav" class="list-group-item border-0 list-group-item-action rounded my-1" :class="{ active : item.url == url}"  :href="item.url">{{item.link}}</a>' +
    '</div>',
})

Vue.component('footer-component', {
props: ['year'],
  template: '<footer><hr /><p class="mt-5">&copy; Copyright 2017-{{year}} MK Turbo. All Rights Reserved.</p></footer>',
})

Vue.component('modal', {
  props: ['modal'],
  template: '<transition name="modal">' +
     '<div class="modal fade show">' +
       '<div class="modal-dialog modal-lg" role="document">' +
         '<div class="modal-content">' +
           '<div class="modal-header">' +
             '<h5 class="modal-title">{{ modal.title }}</h5>' +
             '<button type="button" class="close" @click="$emit(' + "'close'" + ')">' +
               '<span aria-hidden="true">&times;</span>' +
             '</button>' +
           '</div>' +
           '<div class="modal-body text-center">' +
             '<img :src="modal.img" class="img-fluid" :alt="modal.title">' +
             '<p>{{ modal.caption }}</p>' +
           '</div>' +
           '<div class="modal-footer">' +
             '<button type="button" class="btn btn-secondary" @click="$emit(' + "'close'" + ')">Close</button>' +
           '</div>' +
         '</div>' +
       '</div>' +
     '</div></transition>',
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
      url: [],
      isActive: false,
      showModal: false,
      modal: [
        {title: '', caption: '', img: ''},
      ],
      price: {
        NA6DIY: '1,776',
        NA6IC: '2,350',
        NA6Full: '4,090',
        NA8DIY: '1,776',
        NA8IC: '2,350',
        NA8Full: '4,090',
        NBDIY: '1,776',
        NBIC: '2,350',
        NBFull: '4,040',
      },
      NA6pics: [
        {url: 'assets/img/1.6LNA/1.6diykit.jpg', thumb: 'assets/img/1.6LNA/1.6diykit_thumb.jpg', heading: 'MKTurbo DIY Turbo Kit', desc: 'Turbo manifold, T3 Turbo, Downpipe, and Full exhaust', alt: ''},
        {url: 'assets/img/1.6LNA/1.6downpipe.jpg', thumb: 'assets/img/1.6LNA/1.6downpipe_thumb.jpg', heading: '', desc: '', alt: ''},
        {url: 'assets/img/1.6LNA/1.6exhaust.jpg', thumb: 'assets/img/1.6LNA/1.6exhaust_thumb.jpg', heading: '', desc: '', alt: ''},
        {url: 'assets/img/1.6LNA/1.6manifold1.jpg', thumb: 'assets/img/1.6LNA/1.6manifold1_thumb.jpg', heading: '', desc: 'Log-style turbo manifold with a heavy-duty T3 flange that\'s tapped for M10 hardware', alt: ''},
        {url: 'assets/img/1.6LNA/1.6manifoldports.jpg', thumb: 'assets/img/1.6LNA/1.6manifoldports_thumb.jpg', heading: '', desc: 'Port-matched manifold with a smooth transition to the runners for better flow', alt: ''},
        {url: 'assets/img/1.6LNA/1.6fullexhaust.jpg', thumb: 'assets/img/1.6LNA/1.6fullexhaust_thumb.jpg', heading: '', desc: 'Compete custom-bent turbo-back exhaust, with v-bands from end-to-end, and a 5x11x22" Magnaflow muffler for ultimate driving pleasure and performance', alt: ''},
        {url: 'assets/img/1.6LNA/1.6installed.jpg', thumb: 'assets/img/1.6LNA/1.6installed_thumb.jpg', heading: '', desc: 'Turbo fits A/C and p/S without any trimming or massaging any metal', alt: ''},
        {url: 'assets/img/1.6LNA/1.6manifold.jpg', thumb: 'assets/img/1.6LNA/1.6manifold_thumb.jpg', heading: '', desc: '', alt: ''},
        {url: 'assets/img/1.6LNA/1.6hotsidepipe.jpg', thumb: 'assets/img/1.6LNA/1.6hotsidepipe_thumb.jpg', heading: '', desc: '', alt: ''},
        {url: 'assets/img/1.6LNA/1.6intercoolerpies.jpg', thumb: 'assets/img/1.6LNA/1.6intercoolerpies_thumb.jpg', heading: '', desc: '', alt: ''},
        {url: 'assets/img/1.6LNA/1.6piping.jpg', thumb: 'assets/img/1.6LNA/1.6piping_thumb.jpg', heading: '', desc: '', alt: ''},
        {url: 'assets/img/1.6LNA/1.6dyno.jpg', thumb: 'assets/img/1.6LNA/1.6dyno_thumb.jpg', heading: '', desc: '', alt: ''},
      ],
      NA8pics: [
        {url: 'assets/img/1.6LNA/1.6diykit.jpg', thumb: 'assets/img/1.6LNA/1.6diykit_thumb.jpg', heading: 'MKTurbo DIY Turbo Kit', desc: 'Turbo manifold, T3 Turbo, Downpipe, and Full exhaust', alt: ''},
        {url: 'assets/img/1.6LNA/1.6downpipe.jpg', thumb: 'assets/img/1.6LNA/1.6downpipe_thumb.jpg', heading: '', desc: '', alt: ''},
        {url: 'assets/img/1.6LNA/1.6exhaust.jpg', thumb: 'assets/img/1.6LNA/1.6exhaust_thumb.jpg', heading: '', desc: '', alt: ''},
        {url: 'assets/img/1.6LNA/1.6manifold1.jpg', thumb: 'assets/img/1.6LNA/1.6manifold1_thumb.jpg', heading: '', desc: 'Log-style turbo manifold with a heavy-duty T3 flange that\'s tapped for M10 hardware', alt: ''},
        {url: 'assets/img/1.6LNA/1.6manifoldports.jpg', thumb: 'assets/img/1.6LNA/1.6manifoldports_thumb.jpg', heading: '', desc: 'Port-matched manifold with a smooth transition to the runners for better flow', alt: ''},
        {url: 'assets/img/1.6LNA/1.6fullexhaust.jpg', thumb: 'assets/img/1.6LNA/1.6fullexhaust_thumb.jpg', heading: '', desc: 'Compete custom-bent turbo-back exhaust, with v-bands from end-to-end, and a 5x11x22" Magnaflow muffler for ultimate driving pleasure and performance', alt: ''},
        {url: 'assets/img/1.6LNA/1.6installed.jpg', thumb: 'assets/img/1.6LNA/1.6installed_thumb.jpg', heading: '', desc: 'Turbo fits A/C and p/S without any trimming or massaging any metal', alt: ''},
        {url: 'assets/img/1.6LNA/1.6manifold.jpg', thumb: 'assets/img/1.6LNA/1.6manifold_thumb.jpg', heading: '', desc: '', alt: ''},
        {url: 'assets/img/1.6LNA/1.6hotsidepipe.jpg', thumb: 'assets/img/1.6LNA/1.6hotsidepipe_thumb.jpg', heading: '', desc: '', alt: ''},
        {url: 'assets/img/1.6LNA/1.6intercoolerpies.jpg', thumb: 'assets/img/1.6LNA/1.6intercoolerpies_thumb.jpg', heading: '', desc: '', alt: ''},
        {url: 'assets/img/1.6LNA/1.6piping.jpg', thumb: 'assets/img/1.6LNA/1.6piping_thumb.jpg', heading: '', desc: '', alt: ''},
        {url: 'assets/img/NB/NBdyno.jpg', thumb: 'assets/img/NB/NBdyno_thumb.jpg', heading: '', desc: '', alt: ''},
      ],
      NBpics: [
        {url: 'assets/img/NB/NBdiykit.jpg', thumb: 'assets/img/NB/NBdiykit_thumb.jpg', heading: 'MKTurbo DIY Turbo Kit', desc: 'Turbo manifold, T3 Turbo, Downpipe, and Full exhaust', alt: ''},
        {url: 'assets/img//NB/downpipe.jpg', thumb: 'assets/img//NB/downpipe_thumb.jpg', heading: '', desc: '', alt: ''},
        {url: 'assets/img/NB/t3turbo.jpg', thumb: 'assets/img/NB/t3turbo_thumb.jpg', heading: '', desc: '', alt: ''},
        {url: 'assets/img/NB/manifold_angle.jpg', thumb: 'assets/img/NB/manifold_angle_thumb.jpg', heading: '', desc: 'Log-style turbo manifold with a heavy-duty T3 flange that\'s tapped for M10 hardware', alt: ''},
        {url: 'assets/img/NB/manifold_top.jpg', thumb: 'assets/img/NB/manifold_top_thumb.jpg', heading: '', desc: '', alt: ''},
        {url: 'assets/img/NB/muffler.jpg', thumb: 'assets/img/NB/muffler_thumb.jpg', heading: '', desc: 'Compete custom-bent turbo-back exhaust, with v-bands from end-to-end, and a 5x11x22" Magnaflow muffler for ultimate driving pleasure and performance', alt: ''},
        {url: 'assets/img/NB/NBinstalled.jpg', thumb: 'assets/img/NB/NBinstalled_thumb.jpg', heading: '', desc: 'Turbo fits A/C and p/S without any trimming or massaging any metal', alt: ''},
        {url: 'assets/img/NB/NBintercoolerhotside.jpg', thumb: 'assets/img/NB/NBintercoolerhotside_thumb.jpg', heading: '', desc: '', alt: ''},
        {url: 'assets/img/NB/NBintercoolerbracket.jpg', thumb: 'assets/img/NB/NBintercoolerbracket_thumb.jpg', heading: '', desc: '', alt: ''},
        {url: 'assets/img/NB/NB2intercoolerkit.jpg', thumb: 'assets/img/NB/NB2intercoolerkit_thumb.jpg', heading: '', desc: '', alt: ''},
        {url: 'assets/img/NB/intercooler.jpg', thumb: 'assets/img/NB/intercooler_thumb.jpg', heading: '', desc: '', alt: ''},
        {url: 'assets/img/NB/bov.jpg', thumb: 'assets/img/NB/bov_thumb.jpg', heading: '', desc: '', alt: ''},
        {url: 'assets/img/NB/NBexhaustpacked.jpg', thumb: 'assets/img/NB/NBexhaustpacked_thumb.jpg', heading: '', desc: 'Professional-level packing with double-walled custom-built cardboard boxes to ensure your parts arrive without damage', alt: ''},
        {url: 'assets/img/NB/NBdyno.jpg', thumb: 'assets/img/NB/NBdyno_thumb.jpg', heading: '', desc: '', alt: ''},
      ],
      slide: 0,
      sliding: null
  	};
	},

  created: function() {
   this.fetchData();
  },
  methods: {
   fetchData: function() {
      var d = new Date();
      this.year = d.getFullYear();
      this.url = window.location.href.split('/').pop();
   },
   makeActive: function() {
      this.isActive = !this.isActive;
   },
   onSlideStart (slide) {
      this.sliding = true
    },
    onSlideEnd (slide) {
      this.sliding = false
    }
  }
})
