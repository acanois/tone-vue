<template>
  <div id="container" class="threeContainer"></div>
</template>

<script>
import Vue from "vue";
import * as THREE from "three";
import * as VueGL from "vue-gl";

// Imports vue-gl html tags
Object.keys(VueGL).forEach(name => Vue.component(name, VueGL[name]));

function initCamera () {
  return new THREE.PerspectiveCamera(70, container.clientWidth / 480, 0.01, 100);
}

function initScene () {
  return new THREE.Scene()
}

function initRenderer () {
  const renderer = new THREE.WebGLRenderer({ antialias: true })
  renderer.setSize(container.clientWidth, 480)

  return renderer
}

function initMesh () {
  const geometry = new THREE.BoxGeometry(1, 1, 1);
  const material = new THREE.MeshNormalMaterial();
  const mesh = new THREE.Mesh(geometry, material);

  return mesh
}

function renderScene () {
  requestAnimationFrame(this.renderScene)
  this.mesh.rotation.x += 0.01
  this.mesh.rotation.z += 0.01
  this.renderer.render(this.scene, this.camera)
}

export default {
  name: "Graphics",
  mounted: function() {
    this.camera = initCamera()
    this.scene = initScene()
    this.mesh = initMesh()
    this.renderer = initRenderer()

    this.camera.position.z = 10

    this.scene.add(this.mesh)

    document.getElementById('container').appendChild(this.renderer.domElement)

    this.renderScene()
  },
  methods: {
    initCamera,
    initScene,
    initRenderer,
    initMesh,
    renderScene
  }
};
</script>

<style>
#container {
  margin-top: 60px;
  width: 100%;
  height: 100%;
}
</style>