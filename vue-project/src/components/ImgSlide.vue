<template>
    <div class="sliderWrap">
        <p class="left" @click="toLeft">
            <img src="../assets/right.png" alt="" />
        </p>
        <p class="right" @click="toRight">
            <img src="../assets/right.png" alt="" />
        </p>
        <p class="imgText">
            {{ activateImg.name }}
        </p>
        
        <img :src="activateImg.src" :alt="activateImg.name" :style="{width:`${width}px`, height:`${height}px`}" />

        <div class="dot">
            <span @click="setActive(0)" :class="{active:currIdx === 0}">1</span>
            <span @click="setActive(1)" :class="{active:currIdx === 1}">2</span>
            <span @click="setActive(2)" :class="{active:currIdx === 2}">3</span>
        </div>
    </div>
</template>

<script>
import { computed, ref } from 'vue';

// 1. 부모에게 받은 데이터 등록 사용 할 수 있도록 하기
// 2. 기본틀 스타일 작성

export default {
    props:{
        option:{
            type: Object,
            required: true
            // props 내용이 없을 경우에 에러 발생시킴, 필수사항 지정하기
        }
    },
    setup (props) {
        let currIdx = ref(0);
        // => 현재 이미지가 몇번째 이미지인지 확인
        const toLeft = () => {
            currIdx.value = Math.max(currIdx.value-1,0)
        };
        const toRight = () => {
            currIdx.value = Math.min(
                currIdx.value+1,
                props.option.list.length-1
            )
        };
        const setActive = (idx) => {
            currIdx.value = idx
        };  
        const activateImg = computed(()=> props.option.list[currIdx.value]);
        const width = computed(()=>props.option.width);
        const height = computed(()=>props.option.height);

        return {
            toLeft,
            toRight,
            setActive,
            currIdx,
            activateImg,
            width,
            height
        }
    }
}
</script>
<!-- scoped 통합 스타일을 하나의 .vue 영역으로 고정시킬때 
다른 .vue 파일에서 동일 스타일 명을 사용해도 서로 다른것으로 인식-->
<style lang="css" scoped>
/* 부모영역
- 부모 영역에 크기 값 지정
- overflow 값 지정
- margin 중앙 설정하기 */

/* 버튼영역
- 부모 안에서 위치 설정
- css 회전 rotate:180deg
- :hover css 마우스 오버 효과
- transition: all 1s
- .active 활성화 작업*/

.sliderWrap {
    width: 1000px;
    overflow: hidden;
    position: relative;
    margin: 0 auto;
    margin-top: 20px;
}
.sliderWrap>p {
    position: absolute;
    top: 50%;
    font-size: 20px;
    /* transition: all 2s left ease; */
}
.sliderWrap span:hover {
    cursor: pointer;
}

.imgText {
  width: 400px;
  height: 50px;
  position: absolute;
  /* => 자식이 절대값 위치 */
  margin-top: 150px;
  left: 50%;
  margin-left: -200px;
  background: rgba(226, 226, 226, 0.4);
  color: rgb(0, 0, 0);
  padding: 10px;
  z-index: 100;
}
img {
    position: relative;
    left: 50%;
    margin-left: -225px;
    /* transition: all 2s left ease; */
}

p.left {
    width: 50px;
    height: 50px;
    left: 0px;
    rotate: 180deg;
}
p.right {
    width: 50px;
    height: 50px;
    right: 0px;
}
p.left>img, p.right>img{
    width: 100%;
    height: 100%;
}
.dot {
    width: 100px;
    position: absolute;
    left : 50%;
    margin-left: -50px;
    bottom: 10px;
}
.dot>span {
    width: 12px;
    height: 12px;
    margin: 0 4px;
    background-color: blanchedalmond;
    border-radius: 6px;
    display: inline-block;
    transition: all 2s ease;
    /* box-shadow: inset 0 1px 1px 0px rgb(0 0 0 / 60%), 0px 1px 1px 0px white; */
}
.dot > span:hover,
.dot>span.active {
    cursor: pointer;
    background-color: aliceblue;
}


</style>