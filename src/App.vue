<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
    name: 'App'
    ,mounted(){
        this.setFs()
    }
    ,methods: {
        setFs(){
            var html = document.documentElement;
            function setFont() {
                var cliWidth = html.clientWidth;
                html.style.fontSize = 100 * (cliWidth / 750) + 'px';
            }
            setFont();

            window.addEventListener('resize', setFont, false);
        }
    }
}

</script>

<style>
* {margin:0;padding:0;list-style:none;}
body {font-family: verdana, arial;color:#2c3e50;-webkit-font-smoothing: antialiased;background-color:#222;
    font-size:.24rem;}
</style>
