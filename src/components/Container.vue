<template>
    <div>
        <div v-if="step ==0">
            <Post :게시물 ="게시물[i]" v-for="(a,i) in 게시물" :key="i"/>
        </div>

        <div v-if="step ==1">
    <!-- 필터선택페이지 -->
        <div class="upload-image" style="`background-image:url(${이미지})`"></div>
        <div class="filters">
            <filterBox :필터="필터" :이미지="이미지" v-for="필터 in filters" :key="필터">
                <template v-slot:a><span>데이터1</span></template>
                <template v-slot:b>데이터2</template>
            </filterBox>


        </div
    </div>

    <!-- 글작성페이지 -->
    <div v-if="step ==2">
        <div class="upload-image"></div>
            <div class="write">
                <textarea @input="$emit('write', $event.target.value)" class="write-box">write!</textarea>
            </div>
        </div>
    </div>
</template>

<script>
import Post from './Post.vue'
import FilterBox from './FiltetBox.vue'

export default{
    data(){
        return{
            filters : [ "aden", "_1977", "brannan", "brooklyn", "clarendon", "earlybird", "gingham", "hudson", "inkwell", "kelvin", "lark", "lofi", "maven", "mayfair", "moon", "nashville", "perpetua", "reyes", "rise", "slumber", "stinson", "toaster", "valencia", "walden", "willow", "xpro2"],
        }
    },

    components :{
        Post,
        FilterBox,
    },
    props :{
        게시물 : Array,
        step : Number,
        이미지 : String,
    },
}
</script>

<style>
.upload-image{
width: 100%;
height: 450px;
background: cornflowerblue;
background-size : cover;
}
.filters{
overflow-x:scroll;
white-space: nowrap;
}
.filter-1 {
width: 100px;
height: 100px;
background-color: cornflowerblue;
margin: 10px 10px 10px auto;
padding: 8px;
display: inline-block;
color : white;
background-size: cover;
}
.filters::-webkit-scrollbar {
height: 5px;
}
.filters::-webkit-scrollbar-track {
background: #f1f1f1; 
}
.filters::-webkit-scrollbar-thumb {
background: #888; 
border-radius: 5px;
}
.filters::-webkit-scrollbar-thumb:hover {
background: #555; 
}
.write-box {
border: none;
width: 90%;
height: 100px;
padding: 15px;
margin: auto;
display: block;
outline: none;
}
</style>