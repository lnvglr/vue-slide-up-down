<template>
	<h1>Vue SlideUpDown</h1>
	<input v-model="noSettings" type="checkbox" id="no-settings" />
	<label for="no-settings">Click me!</label>
	<slide-up-down>
		<div v-if="noSettings"><div class="box"><pre class=""><code>{{noSettingsMarkup}}</code></pre></div></div>
	</slide-up-down>

	<hr>

	<h3>List</h3>
	<p>If collapsing margins give you a head ache, try to give the wrapper a <code>display: flex;</code>.</p>
	<div class="options">
		<div v-for="item in expand" :key="item.label">
			<input v-model="item.value" type="checkbox" :id="item.label" />
			<label :for="item.label">{{item.label}}</label>
		</div>
	</div>
	<div class="flex">
		<slide-up-down v-for="item in expand" :key="item.label" class="box white">
			<div v-if="item.value"><div v-html="item.text" class="content"></div></div>
		</slide-up-down>
	</div>

	<hr>

	<h3>Props</h3>
	<input v-model="opacity" type="checkbox" id="props" />
	<label for="props">Show/Hide</label><br><br>
	<div class="">
	<div class="input-group"><label for="opacity">Opacity</label>
	<input v-model="opacityValue" type="number" min="0" max="1" step="0.1" placeholder="Opacity" id="opacity"/></div>
	<div class="input-group"><label for="scale">Scale</label>
	<input v-model="scaleValue" type="number" min="0" max="5" step="0.01" placeholder="scale" id="scale"/></div>
	<div class="input-group"><label for="duration">Duration</label>
	<input v-model="durationValue" type="number" min="0" max="10000" step="100" placeholder="duration" id="duration"/></div>
	<div class="input-group"><label for="timing">Timing</label>
	<input v-model="timingValue" type="text" placeholder="timing" id="timing"/></div>
	</div>
		<slide-up-down
		:opacity="opacityValue"
		:scale="scaleValue"
		:duration="durationValue"
		:timing="timingValue"
	>
		<div v-if="opacity"><p>
		<pre><code>props: {
  opacity: {
    type: Number,
    default: 0
  },
  scale: {
    type: Number,
    default: 0.9
  },
  duration: {
    type: Number,
    default: 300
  },
  timing: {
    type: String,
    default: "ease-in-out"
  }
}</code></pre>
	</p></div>
	</slide-up-down>
	<div style="margin-bottom: 80vh;"></div>
</template>

<script>
import SlideUpDown from "./components/SlideUpDown.vue";

export default {
	name: "App",
	components: {
		SlideUpDown,
	},
	data() {
		return {
			noSettings: false,
			noSettingsMarkup: `<input v-model="value" type="checkbox" id="example" />
<label for="example">Click me!</label>
<slide-up-down>
  <div v-if="value"><div class="box">I am no longer hidden.</div></div>
</slide-up-down>`,
			opacity: false,
			opacityValue: 0.5,
			scaleValue: 0.9,
			durationValue: 1000,
			timingValue: "cubic-bezier(0.47, 0, 0.175, 1)",
			expand: [
				{
					value: false,
					label: "Options A",
					text: "Lorem Ipsum",
				},
				{
					value: false,
					label: "Options B",
					text:
						"<img src='https://images.unsplash.com/photo-1526526431900-88eb525f1e4a?ixlib=rb-1.2.1&ixid=MXwxMjA3fDB8MHxwaG90by1yZWxhdGVkfDh8fHxlbnwwfHx8&auto=format&fit=crop&w=500&q=60' /><span>Caption</span>",
				},
				{
					value: false,
					label: "Options C",
					text:
						"It can have a lot of text and still expands very smoothly. Smooth: having an even and regular surface; free from perceptible projections, lumps, or indentations.",
				},
			]
		};
	},
};
</script>

<style>
* {
	box-sizing: border-box;
}
body {
	background: #fefefe;
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	color: #2c3e50;
	padding: 50px;
	width: 640px;
	max-width: 90%;
	margin: 0 auto;
}
hr {
	margin: 50px 0;
	border: 1px solid #f0f0f0;
}
pre {
	overflow-x: auto;
	border-radius: 5px;
	position: relative;
}
pre code {
	overflow-x: auto;
	color: #525252;
	white-space: pre;
	padding: 1.2em 1.4em;
	font-size: 0.85rem;
	line-height: 1.6rem;
	display: block;
}
code,
pre {
	font-family: "Roboto Mono", Monaco, courier, monospace;
	font-size: 0.85em;
	background-color: #f8f8f8;
	-webkit-font-smoothing: initial;
	-moz-osx-font-smoothing: initial;
}
code {
	color: #d63200;
	padding: 3px 5px;
	margin: 0 2px;
	border-radius: 2px;
	white-space: nowrap;
}
.flex {
	display: flex;
	flex-direction: column;
}
.flex.row {
	flex-direction: row;
}
.flex.wrap {
	flex-wrap: wrap;
	gap: 1em;
}
.box {
	margin: 10px 0;
}
.box.white {
	border-radius: 5px;
	background: #fff;
	box-shadow: inset 0 0 0 1px #f0f0f0;
	padding: 0px;
}
.options {
	display: flex;
	gap: 1em;
}
.content {
	padding: 50px;
}
.input-group {
	display: flex;
	flex-direction: column;
	margin-bottom: 1em
}
.input-group label {
	margin-right: 1em;
}
input[type="number"],
input[type="text"] {
	padding: 10px;
}
.content img {
	display: block;
	width: calc(100% + 100px);
	margin: -50px;
	border-radius: 5px 5px 0 0;
}
.content img:not(:last-child) {
	margin-bottom: 50px;
}
</style>
