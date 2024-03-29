<template>
    <div class="intro">
        <div class="intro__blind intro__blind--1"></div>
        <div class="intro__blind intro__blind--2"></div>
        <div class="intro__blind intro__blind--3"></div>
        <div class="intro__blind intro__blind--4"></div>
        <span class="intro__line intro__line--1"></span>
        <span class="intro__line intro__line--2"></span>
        <span class="intro__line intro__line--3"></span>
        <div class="container container--lg">
            <div class="intro__inner">
                <h2 class="intro__tit intro__ani tit--lg"><span>{{ portfolios[0].tit }}</span></h2>
                <div class="intro__ani-group">
                    <h2 class="intro__ani tit--lg"><span>CREATIVE</span></h2>
                    <h2 class="intro__ani tit--lg"><span>WEB PUBLISHER</span></h2>
                    <h2 class="intro__ani tit--lg"><span>I'M READY</span></h2>
                </div>
            </div>
        </div>
    </div>
  </template>
  
  <script>
  import { portfolios } from "@/assets/data/portfolio.js"

  export default {
    components: {
    },
    data() {
        return {
          portfolios,  
        };
    },
  }
  </script>
  