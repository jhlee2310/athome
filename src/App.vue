<template>
	<div id="wrap">
		<div id="viewport"></div>
		<div style="background-color:white;color:black">some</div>
	</div>
</template>
<script>
  import Ani from '@/assets/js/animate.js'
  import * as THREE from 'three' 
	
	const $3d = new (function(){
		this.scene = null;
		this.camera = null,
		this.aspect = null;
		this.frustumSize = 5;

		this.onWindowResize = ()=>{
			let frustumSize = this.frustumSize;
			let aspect = this.aspect = window.innerWidth / window.innerHeight;		
			this.renderer.setSize( window.innerWidth, window.innerHeight );
			this.camera.left = -  frustumSize * aspect / 2;
			this.camera.right =  frustumSize * aspect / 2;
			this.camera.top = frustumSize / 2;
			this.camera.bottom = - frustumSize / 2;
			this.camera.updateProjectionMatrix();		
		}

	})()
  
  export default{    
    data(){
      return{
   
      }
    },
    methods: {
      
    },      
        
    mounted(){ 	
		var frustumSize = $3d.frustumSize
		var aspect = $3d.aspect = window.innerWidth / window.innerHeight		
		var scene = $3d.scene = new THREE.Scene();
		var camera = $3d.camera = new THREE.OrthographicCamera(  frustumSize * aspect / - 2,  frustumSize * aspect / 2, frustumSize / 2, frustumSize / - 2, 1, 1000 );
		camera.position.z = 3
		var renderer = $3d.renderer = new THREE.WebGLRenderer();		 				
		scene.add( camera );
		
		renderer.setSize( window.innerWidth, window.innerHeight );		
		document.querySelector('#viewport').appendChild( renderer.domElement );
		window.addEventListener('resize',$3d.onWindowResize,false)

		var geometry = new THREE.BoxGeometry( 1, 1, 1 );
		var material = new THREE.MeshBasicMaterial( { color: 0x00ff00 } );
		var cube = new THREE.Mesh( geometry, material );
		scene.add( cube );

		let fps = 30;
		let s_time = null;
		let timestep = 1000/fps;
		let cnt = 1;

		function animate(_t) {			
			requestAnimationFrame(animate);

			if (!s_time) s_time = _t;
			if (_t - s_time < timestep) {return;}
			s_time = _t			
			console.log(cnt++);
		}

		animate()
	

    },    
  }
</script>
<style>
*{margin:0;padding:0}
html,body{height:100%}
body{line-height:1;background-color: black}
canvas{display:block}
#viewport{position:absolute;z-index:-9999}
</style>