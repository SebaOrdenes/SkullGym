<template>
<body>
   <!--  <h1>   <img src='../assets/logo.png'></h1> -->
<!-- You can add more ".slideshow-image" elements, but remember to update the "$items" variable on SCSS -->
<div class="slideshow">
   
  <div class="slideshow-image" style="background-image: url('https://images.pexels.com/photos/841130/pexels-photo-841130.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=750&w=1260')"></div>
   <div class="slideshow-image" style="background-image: url('https://c0.wallpaperflare.com/preview/190/596/906/active-adult-body-body-building.jpg')"></div>
  <div class="slideshow-image" style="background-image: url('https://images.pexels.com/photos/136404/pexels-photo-136404.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=750&w=1260')"></div>
  <div class="slideshow-image" style="background-image: url('https://cdn.pixabay.com/photo/2018/06/27/22/45/fitness-3502830_960_720.jpg')"></div>
</div>
</body>
</template>

<style lang="scss" scoped>
$items: 4;
$animation-time: 3s;
$transition-time: .8s;
$scale: 20%;

$total-time: ($animation-time * $items);
$scale-base-1: (1 + $scale / 100%);

.slideshow {
  position: relative;
  width: 100vw;
  height: 100vh;
  overflow: hidden;
}

.slideshow-image {
  position: absolute;
  width: 100%;
  height: 100%;
  background: no-repeat 50% 50%;
  background-size: cover;
  animation-name: kenburns;
  animation-timing-function: linear;
  animation-iteration-count: infinite;
  animation-duration: $total-time;
  opacity: 1;
  transform: scale($scale-base-1);

  @for $i from 1 through $items {
    &:nth-child(#{$i}) {
      animation-name: kenburns-#{$i};
      z-index: ($items - $i);
    }
  }
}

@for $i from 1 through $items {
  @keyframes kenburns-#{$i} {
    $animation-time-percent: percentage($animation-time / $total-time);
    $transition-time-percent: percentage($transition-time / $total-time);
    
    $t1: ($animation-time-percent * ($i - 1) - $transition-time-percent / 2);
    $t2: ($animation-time-percent * ($i - 1) + $transition-time-percent / 2);
    @if($t1 < 0%) { $t1: 0%; }
    @if($t2 < 0%) { $t2: 0%; }

    $t3: ($animation-time-percent * ($i) - $transition-time-percent / 2);
    $t4: ($animation-time-percent * ($i) + $transition-time-percent / 2);
    @if($t3 > 100%) { $t3: 100%; }
    @if($t4 > 100%) { $t4: 100%; }

    $t5: (100% - $transition-time-percent / 2);
    $t6: (($t4 - $t1) * 100% / $t5);

    #{$t1} { opacity: 1; transform: scale($scale-base-1); }
    #{$t2} { opacity: 1; }
    #{$t3} { opacity: 1; }
    #{$t4} { opacity: 0; transform: scale(1); }
    
    @if($i != $items) {
      100% { opacity: 0; transform: scale($scale-base-1); }
    }
    
    @if($i == 1) {
      $scale-plus: ($scale * (100% - $t5) / $t4);
      $scale-plus-base-1: (1 + ($scale + $scale-plus) / 100%);
    
      #{$t5} { opacity: 0; transform: scale($scale-plus-base-1); }
      100% { opacity: 1; }
    }
  }
}


// Presentational stuff
h1 {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate3d(-50%, -50%, 0);
  z-index: 99;
  text-align: center;
  font-family: Raleway, sans-serif;
  font-weight: 300;
  text-transform: uppercase;
  background-color: none;
     background-size:100% auto;
  box-shadow: 0 1em 2em -1em rgba(0,0,0,.5);
  padding: 1em 2em;
  line-height: 1.5;

  .medium{
       display: block;
    text-transform: lowercase;
    font-size: .7em;
    box-shadow: 0 1em 2em -1em rgba(245, 243, 243, 0.5); 

      
  }
  small {
    display: block;
    text-transform: lowercase;
    font-size: .7em;
    
    &:first-child {
      border-bottom: 1px solid rgba(0,0,0,.25);
      padding-bottom: .5em;
    }
    
    &:last-child {
      border-top: 1px solid rgba(0,0,0,.25);
      padding-top: .5em;
    }
  }
}

</style>
