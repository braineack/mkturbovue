Vue.component('base-layout', {
  props: ['isActive', 'makeActive' ],
  template:
  '<b-container>' +
    '<header>' +
      '<slot name="header"></slot>' +
    '</header>' +
    '<main>' +
      '<b-row class="row-offcanvas row-offcanvas-left" :class="{active: isActive}">' +
        '<b-col class="sidebar-offcanvas" cols="6" md="3">' +
          '<slot name="navigation"></slot>' +
        '</b-col>' +
        '<p class="float-left d-sm-block d-md-none pl-3">' +
          '<button type="button" class="btn btn-pink btn-sm" data-toggle="offcanvas" @click="makeActive()">Toggle nav  &raquo;</button>' +
        '</p>' +
        '<b-col cols="12" md="9">' +
         '<slot></slot>' +
        '</b-col>'+
      '</b-row>'+
    '</main>' +
    '<footer>' +
      '<slot name="footer"></slot>' +
    '</footer>' +
  '</b-container>'
})

Vue.component('navbar-component', {
  props: ['tagline'],
  template: '<b-navbar type="dark" variant="dark" fixed="top">' +
                '<b-navbar-brand href="index.html">' +
                  '<img src="assets/img/MKTURBO_PinkLogo150x30.png" class="d-inline-block align-top" alt="MKTurbo Logo"/>' +
                  '<span class="pl-3 d-none d-sm-inline">{{tagline}}</span>' +
                  '</b-navbar-brand>' +
             '</b-navbar>',
})


Vue.component('sidebar-offcanvas', {
props: ['nav', 'url'],
  template:'<b-list-group>' +
              '<b-list-group-item v-for="item in nav" class="border-0 rounded my-1" :key="item.key" :active="item.url == url ? true : false" :href="item.url">{{item.link}}</b-list-group-item>' +
            '</b-list-group>',
})

Vue.component('footer-component', {
props: ['year'],
  template: '<div><hr /><p class="mt-5">&copy; Copyright 2017-{{year}} MK Turbo. All Rights Reserved.</p></div>',
})

Vue.component('sale-banner', {
  props: ['active', 'price'],
  template: '<div class="jumbotron saleimage">' +
                '<div class="container">' +
                '<h3 class="display-4">Red, White, and <span class="text-pink font-weight-bold">BOOST</span> sale!</h3>' +
                  '<h4 class="mb-2">Celebrating 1776 with savings on boost</h4>' +
                  '<p class="mb-2 lead">Complete Turbo Kits <span class="text-pink lead"><strong>{{ price.NA6Full.dis }}</strong></span> shipped!</p>' +
                  '<p class="mb-2 lead">NA/NB DIY Turbo Kits for <span class="text-pink lead"><strong>{{ price.NA6DIY.dis }}</strong></span> shipped!</p>' +
                  '<hr class="my-4">' +
                  '<a class="btn btn-pink mr-3 mb-3" href="9093NA6.html" role="button">90-93 NA6 »</a>' +
                  '<a class="btn btn-pink mr-3 mb-3" href="9097NA8.html" role="button">90-97 NA8  »</a>' +
                  '<a class="btn btn-pink mb-3" href="9905NB.html" role="button">99-05 NB1/NB2  »</a>' +
                '</div>' +
            '</div>'
})


Vue.component('modal', {
  props: ['modal'],
  template: '<transition name="modal">' +
     '<div class="modal fade show" @click="$emit(' + "'close'" + ')">' +
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
             '<a :href="modal.fullSize" target="_blank" v-if="modal.full"><button type="button" class="btn btn-secondary">View Full Size</button></a>' +
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
        {title: '', caption: '', img: '', fullSize: '', full: false},
      ],
      price: {
        NA6DIY: {reg: '1,776', dis: '1,500', sale: false},
        NA6IC: {reg: '2,350', dis: '2,250', sale: false},
        NA6Full: {reg: '4,090', dis: '4,000', sale: false},
        NA8DIY: {reg: '1,776', dis: '1,500', sale: false},
        NA8IC: {reg: '2,350', dis: '2,250', sale: false},
        NA8Full: {reg: '4,040', dis: '4,000', sale: false},
        NBDIY: {reg: '1,776', dis: '1,500', sale: false},
        NBIC: {reg: '2,350', dis: '2,250', sale: false},
        NBFull: {reg: '4,040', dis: '4,000', sale: false},
        OilKit: {reg: '125', dis: '110', sale: false},
      },
      saleBannerActive: false,
      parts: {
        NA6DIY: [ '<strong>Welded</strong> Log Style Manifold', '<strong>T3 Turbo</strong> with 2.5" v-band outlet', '<strong>2.5" to 3" Downpipe</strong> with v-bands at either end', '<strong>Full 3" exhaust</strong> with SS Magnaflow muffler\, v-bands for all connections' ],
        NA6IC: [ '<strong>DIY Turbo</strong> Kit', '<strong>18 x 18"</strong> Bar & Plate Intercooler', '<strong>Complete</strong> aluminum piping, silicone couplers, t-clamps, and 3/4" AIT bung', '<strong>BOV</strong> with mated flange on piping' ],
        NA6Full: [ '<strong>Intercooled Turbo</strong> Kit', '<strong>PNP vTPS</strong> Plug-N-Play variable TPS', '<strong>Cone Filter</strong> with intake piping', '<strong>640cc </strong> Force Flow EV-14 Injectors', '<strong>MS3PRO ECU</strong> Plug-N-Play Standalone Engine Management System', '<strong>WBo2</strong> Controller w/ sensor', '<strong>Oil Line Kit</strong> feed line\, drain line\, and fittings' ],
        NA8DIY: [ '<strong>Welded</strong> Log Style Manifold', '<strong>T3 Turbo</strong> with 2.5" v-band outlet', '<strong>2.5" to 3" Downpipe</strong> with v-bands at either end', '<strong>Full 3" exhaust</strong> with SS Magnaflow muffler\, v-bands for all connections', '<strong>EGR block off plates</strong> for both ports' ],
        NA8IC: [ '<strong>DIY Turbo</strong> Kit', '<strong>18 x 18"</strong> Bar & Plate Intercooler', '<strong>Complete</strong> aluminum piping, silicone couplers, t-clamps, and 3/4" AIT bung', '<strong>BOV</strong> with mated flange on piping' ],
        NA8Full: [ '<strong>Intercooled Turbo</strong> Kit', '<strong>Cone Filter</strong> with intake piping', '<strong>640cc </strong> Force Flow EV-14 Injectors', '<strong>MS3PRO ECU</strong> Plug-N-Play Standalone Engine Management System', '<strong>WBo2</strong> Controller w/ sensor', '<strong>Oil Line Kit</strong> feed line\, drain line\, and fittings' ],
        NBDIY: [ '<strong>Welded</strong> Log Style Manifold', '<strong>T3 Turbo</strong> with 2.5" v-band outlet', '<strong>2.5" to 3" Downpipe</strong> with v-bands at either end', '<strong>Full 3" exhaust</strong> with SS Magnaflow muffler\, v-bands for all connections', '<strong>EGR block off plates</strong> for both ports' ],
        NBIC: [ '<strong>DIY Turbo</strong> Kit', '<strong>18 x 18"</strong> Bar & Plate Intercooler', '<strong>Complete</strong> aluminum piping, silicone couplers, t-clamps, and 3/4" AIT bung', '<strong>BOV</strong> with mated flange on piping' ],
        NBFull: [ '<strong>Intercooled Turbo</strong> Kit', '<strong>Cone Filter</strong> with intake piping', '<strong>640cc </strong> Force Flow EV-14 Injectors', '<strong>MS3PRO ECU</strong> Plug-N-Play Standalone Engine Management System', '<strong>WBo2</strong> Controller w/ sensor', '<strong>Oil Line Kit</strong> feed line\, drain line\, and fittings' ],
        OilKit: [ '<strong>TSE</strong> oil feed adapter and -4an fitting', '<strong>SS Oil feed line</strong> -4an', '<strong>Fitting and flange</strong> for turbo oil inlet and outlet', '<strong>SS Oil drain line</strong> -8an', '<strong>SS Drain-pan fitting</strong> 3/8npt to -8an', ],
      },
      NA6pics: [
        {dir: 'assets/img/product/', url: 'NBdiykit.jpg', heading: 'MKTurbo DIY Turbo Kit', desc: 'Turbo manifold, T3 Turbo, Downpipe, and Full exhaust', alt: ''},
        {dir: 'assets/img/product/', url: 'downpipe.jpg', heading: 'MKTurbo Downpipe', desc: '2.5" to 3" downpipe with flex and WB bung', alt: ''},
        {dir: 'assets/img/product/', url: 't3turbo.jpg', heading: 'MKTurbo 50trim T3 Turbo', desc: 'Capable, quick-spooling turbo that can support 250/250 hp/tq', alt: ''},
        {dir: 'assets/img/product/', url: 'manifold_angle.jpg', heading: 'MKTurbo Log Manifold', desc: 'Log-style turbo manifold with a heavy-duty T3 flange that\'s tapped for M10 hardware', alt: ''},
        {dir: 'assets/img/product/', url: 'manifold_top.jpg', heading: 'MKTurbo Log Manifold', desc: 'Log-style turbo manifold with a heavy-duty T3 flange that\'s tapped for M10 hardware', alt: ''},
        {dir: 'assets/img/product/', url: 'muffler.jpg', heading: 'MKTurbo Exhaust', desc: 'Compete custom-bent turbo-back exhaust, with v-bands from end-to-end, and a 5x11x22" Magnaflow muffler for ultimate driving pleasure and performance', alt: ''},
        {dir: 'assets/img/product/', url: '16installed.jpg',  heading: 'MKturbo Installed', desc: 'Turbo fits A/C and p/S without any trimming or massaging any metal', alt: ''},
        {dir: 'assets/img/product/', url: 'NBintercoolerbracket.jpg', heading: 'MKTurbo Intercooler', desc: 'Intercooler mounts up to factory bolt points for easy installation', alt: ''},
        {dir: 'assets/img/product/', url: 'NAintercoolerkit.jpg', heading: 'MKTurbo Intercooler Kit', desc: 'Complete intercooler kit with brackets, AIT bung, BOV port, high-quality silicone and t-clamps', alt: ''},
        {dir: 'assets/img/product/', url: 'intercooler.jpg', heading: 'MKTurbo Intercooler', desc: '18 x 18\" Bar & Plate Intercooler', alt: ''},
        {dir: 'assets/img/product/', url: 'bov.jpg', heading: 'MKTurbo BOV', desc: 'BOV with mated flange on piping', alt: ''},
        {dir: 'assets/img/product/', url: 'NBexhaustpacked.jpg', heading: 'MKTurbo Delivered', desc: 'Professional-level packing with double-walled custom-built cardboard boxes to ensure your parts arrive without damage', alt: ''},
        {dir: 'assets/img/product/', url: '16dyno.jpg',  heading: 'MKTurbo 1.6L Dyno', desc: '', alt: ''},
      ],
      NA8pics: [
        {dir: 'assets/img/product/', url: 'NBdiykit.jpg', heading: 'MKTurbo DIY Turbo Kit', desc: 'Turbo manifold, T3 Turbo, Downpipe, and Full exhaust', alt: ''},
        {dir: 'assets/img/product/', url: 'downpipe.jpg', heading: 'MKTurbo Downpipe', desc: '2.5" to 3" downpipe with flex and WB bung', alt: ''},
        {dir: 'assets/img/product/', url: 't3turbo.jpg', heading: 'MKTurbo 50trim T3 Turbo', desc: 'Capable, quick-spooling turbo that can support 250/250 hp/tq', alt: ''},
        {dir: 'assets/img/product/', url: 'manifold_angle.jpg', heading: 'MKTurbo Log Manifold', desc: 'Log-style turbo manifold with a heavy-duty T3 flange that\'s tapped for M10 hardware', alt: ''},
        {dir: 'assets/img/product/', url: 'manifold_top.jpg', heading: 'MKTurbo Log Manifold', desc: 'Log-style turbo manifold with a heavy-duty T3 flange that\'s tapped for M10 hardware', alt: ''},
        {dir: 'assets/img/product/', url: 'muffler.jpg', heading: 'MKTurbo Exhaust', desc: 'Compete custom-bent turbo-back exhaust, with v-bands from end-to-end, and a 5x11x22" Magnaflow muffler for ultimate driving pleasure and performance', alt: ''},
        {dir: 'assets/img/product/', url: '16installed.jpg',  heading: 'MKturbo Installed', desc: 'Turbo fits A/C and p/S without any trimming or massaging any metal', alt: ''},
        {dir: 'assets/img/product/', url: 'NBintercoolerbracket.jpg', heading: 'MKTurbo Intercooler', desc: 'Intercooler mounts up to factory bolt points for easy installation', alt: ''},
        {dir: 'assets/img/product/', url: 'NAintercoolerkit.jpg', heading: 'MKTurbo Intercooler Kit', desc: 'Complete intercooler kit with brackets, AIT bung, BOV port, high-quality silicone and t-clamps', alt: ''},
        {dir: 'assets/img/product/', url: 'intercooler.jpg', heading: 'MKTurbo Intercooler', desc: '18 x 18\" Bar & Plate Intercooler', alt: ''},
        {dir: 'assets/img/product/', url: 'bov.jpg', heading: 'MKTurbo BOV', desc: 'BOV with mated flange on piping', alt: ''},
        {dir: 'assets/img/product/', url: 'NBexhaustpacked.jpg', heading: 'MKTurbo Delivered', desc: 'Professional-level packing with double-walled custom-built cardboard boxes to ensure your parts arrive without damage', alt: ''},
        {dir: 'assets/img/product/', url: 'NBdyno.jpg', heading: 'MKTurbo 1.8L Dyno', desc: '', alt: ''},
      ],
      NBpics: [
        {dir: 'assets/img/product/', url: 'NBdiykit.jpg', heading: 'MKTurbo DIY Turbo Kit', desc: 'Turbo manifold, T3 Turbo, Downpipe, and Full exhaust', alt: ''},
        {dir: 'assets/img/product/', url: 'downpipe.jpg', heading: 'MKTurbo Downpipe', desc: '2.5" to 3" downpipe with flex and WB bung', alt: ''},
        {dir: 'assets/img/product/', url: 't3turbo.jpg', heading: 'MKTurbo 50trim T3 Turbo', desc: 'Capable, quick-spooling turbo that can support 250/250 hp/tq', alt: ''},
        {dir: 'assets/img/product/', url: 'manifold_angle.jpg', heading: 'MKTurbo Log Manifold', desc: 'Log-style turbo manifold with a heavy-duty T3 flange that\'s tapped for M10 hardware', alt: ''},
        {dir: 'assets/img/product/', url: 'manifold_top.jpg', heading: 'MKTurbo Log Manifold', desc: 'Log-style turbo manifold with a heavy-duty T3 flange that\'s tapped for M10 hardware', alt: ''},
        {dir: 'assets/img/product/', url: 'muffler.jpg', heading: 'MKTurbo Exhaust', desc: 'Compete custom-bent turbo-back exhaust, with v-bands from end-to-end, and a 5x11x22" Magnaflow muffler for ultimate driving pleasure and performance', alt: ''},
        {dir: 'assets/img/product/', url: 'NBinstalled.jpg', heading: '', desc: 'Turbo fits A/C and p/S without any trimming or massaging any metal', alt: ''},
        {dir: 'assets/img/product/', url: 'NBintercoolerhotside.jpg', heading: '', desc: '', alt: ''},
        {dir: 'assets/img/product/', url: 'NBintercoolerbracket.jpg', heading: 'MKTurbo Intercooler', desc: 'Intercooler mounts up to factory bolt points for easy installation', alt: ''},
        {dir: 'assets/img/product/', url: 'NB2intercoolerkit.jpg', heading: 'MKTurbo Intercooler Kit', desc: 'Complete intercooler kit with brackets, AIT bung, BOV port, high-quality silicone and t-clamps', alt: ''},
        {dir: 'assets/img/product/', url: 'intercooler.jpg', heading: 'MKTurbo Intercooler', desc: '18 x 18\" Bar & Plate Intercooler', alt: ''},
        {dir: 'assets/img/product/', url: 'bov.jpg', heading: 'MKTurbo BOV', desc: 'BOV with mated flange on piping', alt: ''},
        {dir: 'assets/img/product/', url: 'NBexhaustpacked.jpg', heading: 'MKTurbo Delivered', desc: 'Professional-level packing with double-walled custom-built cardboard boxes to ensure your parts arrive without damage', alt: ''},
        {dir: 'assets/img/product/', url: 'NBdyno.jpg', heading: 'MKTurbo 1.8L Dyno', desc: '', alt: ''},
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
    },
    getSize (image, size) {
      var filename = image.split('.')[0];
      var extension = image.split('.')[1];
      return filename + '_' + size + '.' + extension
    }
  }
})
