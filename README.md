
## encodeSVG
通过将SVG图形编码，在css:background-image: url("data:image/svg+xml,encodeddSVG")或者border-image中使用SVG背景图片

此工具是学生时代写前端时候，将SVG图片encode为css background-image的小工具，后面域名已经莫得了，现在估计也没人在用这个工具了，留待以后整理
@todo 迁移到gitee
~~线上工具地址【传送门】:[http://www.xiyoulive.com/encodeSVG](http://www.xiyoulive.com/encodeSVG)~~

用的方便还请给个star
```vue
<template>
	<div>
		<h1>SVG图形编码工具</h1>
		作者：ulooper@aliyun.com
		<p>通过将SVG图形编码，在css:background-image: url("data:image/svg+xml,encode")或者border-image中使用SVG背景图片</p>
		<div class="cont">
		<h4>粘贴SVG代码，格式&lt;svg&gt;...code...&lt;/svg&gt;</h4>
			<textarea v-model="insert" class="con" placeholder="此处粘贴<svg>...code...</svg>"></textarea>
		</div>
		<div class="cont">
		<h4>编码后的代码</h4>
			<textarea v-model="encoded" class="con" placeholder="输出编码"></textarea>
		</div>
		<div class="cont">
		<h4>输出css</h4>
			<textarea v-model="css" class="con" placeholder="输出css"></textarea>
		</div>
		<div class="cont">
			<h4>预览</h4>
			<div class="preview con" id="pre"></div>
		</div>

	</div>
</template>

<script>
	export default {
    data() {
            return {
            	//这里数据绑定
            	insert:'',
            	encoded:'',
            	css:'',
            	}
        },
    watch:{
    	insert:function(val,oldVal){
    		//逻辑
    		let namespaced = this.addNameSpace( val );
    		let escaped = this.encodeSVG( namespaced );
    		this.encoded = escaped;
    		let resCss = 'background-image: url("data:image/svg+xml,' + escaped + '");';
    		this.css = resCss;
    		document.getElementById("pre").setAttribute( "style", resCss );
    	}

    },
    methods:{
    	encodeSVG:function(data){
    		//编码
    		let symbols = /[\r\n"%#()<>?\[\\\]^`{|}]/g;
    		
		    // 单引号防止重编码
		    if ( data.indexOf( '"' ) >= 0 ) {
		        data = data.replace( /"/g, "'" );
		    }
		    data = data.replace( />\s{1,}</g, "><" );
		    data = data.replace( /\s{2,}/g, " " );
		    //这里推荐使用encodeURL
		    return data.replace( symbols, encodeURI );
    	},
    	addNameSpace:function(data){
    		//xmlns='http://www.w3.org/2000/svg必须有
		    if ( data.indexOf( "http://www.w3.org/2000/svg" ) < 0 ) {
		        data = data.replace( /<svg/g, "<svg xmlns='http://www.w3.org/2000/svg'" );
		    }
		    return data;
    	}
    }
}
</script>

<style scoped>
.cont{
	display: block;
	width: 90%;
	margin-left: 5%;
	margin-top: 30px;

}
.con{
	width: 100%;
	height: 60px;
	background-repeat:no-repeat;
}
.preview{
	width: 100%;
	height: 200px;
	border:1px solid rgb(150,150,150); 
}
</style>
```
##作者
ulooper@aliyun.com
