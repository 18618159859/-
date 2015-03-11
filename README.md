<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<style type="text/css">
			body,html{ height: 100%;}
		</style>
		<script src="js/three.js"></script>
		<script>
			function d2a(n){
				return Math.PI*n/180;
			}
			window.onload=function(){	
				
				
				var w=document.documentElement.offsetWidth;
				var h=document.documentElement.offsetHeight;
				//场景
				var scene=new THREE.Scene();
				
				//灯光
				var light=new THREE.DirectionalLight(0xffffff,1,0);
				scene.add(light);
				light.position.set(400,400,500);
				light.lookAt(new THREE.Vector3(0,0,0));
				
				//摄影机
				var camera=new THREE.PerspectiveCamera(45,w/h,0.1,10000);
				scene.add(camera);
				camera.position.set(600,400,300);
				camera.lookAt(new THREE.Vector3(0,0,0));
				
				//物体对象
				var obj0=new THREE.Mesh(
					new THREE.CylinderGeometry(10,10,50),
					new THREE.MeshLambertMaterial({
						color:0x9a9a9a,
						wireframe:0
					})
				);
				scene.add(obj0);
				obj0.rotation.z=d2a(40);
				obj0.position.y=250;
				
				var obj=new THREE.Mesh(
					new THREE.CylinderGeometry(8,8,250,20),
					new THREE.MeshLambertMaterial({
						color:0x3ea1ec,
						wireframe:1
					})
				);
				obj0.add(obj);
				obj.position.y=-120;
				
				var obj2=new THREE.Mesh(
					new THREE.CylinderGeometry(80,80,200,1000),
					new THREE.MeshLambertMaterial({
						color:0xec3e7c,
						wireframe:1
					})
				);
				obj.add(obj2);
				obj2.rotation.x=d2a(90);
				obj2.position.y=-200;
				
				//渲染
				var render=new THREE.WebGLRenderer();
				render.setSize(w, h);
				
				document.body.appendChild(render.domElement);
				
				//render.render(scene, camera);
				
				//运动
				var speed=0;
				function next()
				{
					if(obj0.rotation.z<0)	//左边
					{
						speed+=0.1;
					}
					else
					{
						speed-=0.1;
					}
					obj0.rotation.z+=d2a(speed);
					//obj0.rotation.z+=d2a(1);
					
					render.render(scene, camera);
					
					requestAnimationFrame(next);
				}
				requestAnimationFrame(next);
			
		}
		</script>
	</head>
	<body>

	</body>
</html>
