<template>
  <div id="container" class="threeContainer"></div>
</template>

<script>

import * as THREE from "three"
import OrbitControls from 'three-orbitcontrols'

function initCamera(container) {
  return new THREE.PerspectiveCamera(70, container.clientWidth / 480, 0.01, 100)
}

function initScene () {
  return new THREE.Scene()
}

function initRenderer (container) {
  const renderer = new THREE.WebGLRenderer({ antialias: true })
  renderer.setSize(container.clientWidth, 480)

  return renderer
}

function initMesh () {
  const geometry = new THREE.TetrahedronGeometry(1, 0, 1) 
  const material = new THREE.MeshNormalMaterial()
  const mesh = new THREE.Mesh(geometry, material)
  mesh.scale.set(2, 2, 2)

  return mesh
}

function initControls(camera, domElement) {
  return new OrbitControls(camera, domElement)
}

function renderScene() {
  requestAnimationFrame(this.renderScene)
  this.renderer.render(this.scene, this.camera)
}

export default {
  name: "Graphics",
  mounted: function() {
    const container = document.getElementById('container')

    this.camera = initCamera(container)
    this.scene = initScene()
    this.mesh = initMesh()
    this.renderer = initRenderer(container)
    this.controls = initControls(this.camera, this.renderer.domElement)
    
    this.camera.position.set(0, 0, 10)
    this.controls.update()
    this.scene.add(this.mesh)

    container.appendChild(this.renderer.domElement)

    this.renderScene(this.controls)
  },
  methods: {
    initCamera,
    initScene,
    initRenderer,
    initMesh,
    renderScene
  }
}

</script>

<style>
#container {
  margin-top: 60px;
  width: 100%;
  height: 100%;
}
</style>