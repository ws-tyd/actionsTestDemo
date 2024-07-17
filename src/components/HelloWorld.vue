<template>
	<div>
		<div id="dom" style="background-color: white">
			<img alt="Vue logo" src="../assets/logo.png" />
			<h1>{{ msg }}</h1>
			<button @click="count++">count is: {{ count }}</button>
			<p>Edit <code>components/HelloWorld.vue</code> to test hot module replacement.</p>
		</div>
		<div id="get"></div>
		
		<button @click="getImg">生成图片</button>
	</div>
</template>

<script>
// import domToImage from "dom-to-image";
import { domToPng } from 'modern-screenshot';

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      count: 0
    }
  },
	methods: {
		getImg() {
			// html2canvas(document.querySelector("#dom"),{
			// 	useCORS:true,
			// 	async: true
			// }).then(canvas => {
			// 	let url = canvas.toDataURL("image/png");
			// 	let a = document.createElement("a")
			// 	a.href = url;
			// 	a.download = "英雄海报图"
			// 	a.click()
			// 	document.querySelector("#get").appendChild(canvas)
			// });
			domToPng(document.querySelector('#dom')).then(dataUrl => {
				const link = document.createElement('a')
				link.download = 'screenshot.png'
				link.href = dataUrl
				link.click()
			})
		}
	}
}
</script>
