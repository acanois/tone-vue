/* eslint-disable */
<template>
  <div class="transport">
    <button class="transportControl" @click="startTransport()">
      <slot>Start</slot>
    </button>
    <button class="transportControl" @click="stopTransport()">
      <slot>Stop</slot>
    </button>
    <select id="waveList" @change="changeWave()">
      <option value="Sawtooth">Sawtooth</option>
      <option value="Sine">Sine</option>
      <option value="Square">Square</option>
      <option value="Triangle">Triangle</option>
    </select>
    <input id="cutoff" type="text" @change="changeCutoff()">
  </div>
</template>

<script>

import { Transport, AmplitudeEnvelope, Reverb, PingPongDelay, Filter, Gain, Oscillator, 
         Master, Sequence, Analyser } from 'tone'
// Envelope
const adsr = new AmplitudeEnvelope({
  'attack': 0.005,
  'decay': 0.5,
  'sustain': 0.0,
  'release': 0.8
})

// Reverb
const reverb = new Reverb({
  'preDelay': 0.1,
  'decay': 5.0,
  'wet': 0.5
})

reverb.generate().then(() => {
    
})

// Delay
const delay = new PingPongDelay({
  'delayTime': 0.625,
  'maxDelay': 1,
  'wet': 0.35,
  'feedback': 0
})

// Filter
const filter = new Filter({
  'frequency': 5000,
  'rolloff': -24,
  'Q': 0.0
})

// Gain
const oscGain = new Gain({
  'gain': 0.75
})

// Analyzer
const analyzer = new Analyser({
  type: 'waveform',
  smoothing: 0
})

//====================================================================================
// Create oscillator
const synth = new Oscillator('C2', 'triangle').start()

synth.chain(oscGain, adsr, filter, delay, reverb, analyzer, Master)

const notes = [
  'C2', 'G2', 'Eb2', 'Bb2',
  'C3', 'G3', 'Eb3', 'Bb3',
  'C4', 'G4', 'Eb4', 'Bb4',
  'C5', 'Eb5', 'G5'
]

const sequence = new Sequence((time, note) => {
  note = notes[Math.floor(Math.random() * (notes.length))]
  oscGain.gain.value = (Math.random() * 0.5) + 0.25
  synth.frequency.value = note
  adsr.triggerAttackRelease('16n')
  
  const ampData = analyzer.getValue()
  const ampAvg = arr => arr.reduce((a, b) => a + b, 0) / arr.length
  console.log(Math.abs(ampAvg(ampData)) * 100)
}, notes, '8n')

sequence.humanize = false
sequence.interval = '8n'
sequence.start(0)

//============================================================================
function startTransport() {
  Transport.start()
}

function stopTransport() {
  Transport.stop()
}

function changeWave() {
  const waveSelector = document.getElementById('waveList')
  synth.type = waveSelector.value.toLowerCase()
}

function changeCutoff() {
  const cutoff = document.getElementById('cutoff')
  filter.frequency.value = cutoff.value
}

export default {
  name: 'Transport',
  // props: {
  //   msg: String
  // },
  mounted() {
    
  },
  methods: {
    startTransport,
    stopTransport,
    changeWave,
    changeCutoff
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h3 {
    margin: 40px 0 0;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    display: inline-block;
    margin: 0 10px;
  }
  a {
    color: #42b983;
  }
</style>