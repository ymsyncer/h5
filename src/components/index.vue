<template>
  <div class="wrap">
    <img src="../assets/img/yieyue.png" id="music" class="music" onclick="playPause()">
    <div class="page page0" :class="{show:nowPage==0}">
      <img src="../assets/img/start.png" class="start-img">
      <div class="start-content">
        <a class="btn" @click="showPage(1)">立即开始</a>
      </div>
    </div>
    <div class="page page1" :class="{show:nowPage==1}">
      <div class="upload-content">
        <div class="upload-box"  id="crop_result">
          <img src="../assets/img/touxiang.png" id="imgBox">
        </div>
      </div>
      <div class="upload-footer clearfix">
        <div class="con-3">
          <a id="choose_form_album" class="file_input file_input1">
            <img src="../assets/img/shangchaun.png">
          </a>
        </div>
        <div class="con-4">
          <a id="paizhao" class="file_input">
            <img src="../assets/img/paizhao.png">
          </a>
        </div>
        <div class="con-3">
          <div class="haibao-bg-head upload-btn" @click="showPage(2)">选择性别</div>
        </div>
      </div>
    </div>
    <div class="page page2" :class="{show:nowPage==2}">
      <div class="page2-content clearfix">
        <label for="option0">
          <img src="../assets/img/nan.png">
          <input type="radio" id="option0" name="mode" value = "0"  checked />
          <a class="btn">我是男生</a>
        </label>
        <label for="option1">
          <img src="../assets/img/nv.png">
          <input type="radio" id="option1" name="mode" value = "1"  />
          <a class="btn">我是女生</a>
        </label>
      </div>
      <div class="start-content">
        <a class="btn" @click="showPage(3)">选择背景</a>
      </div>
    </div>
    <div class="page page3" :class="{show:nowPage==3}">
      <div class="positon-center back" @click="showPage(2)"><span></span>返回性别</div>
      <div class="page2-content page3-content clearfix">
        <label for="option3">
          <input type="radio" id="option3" name="mode1" value = "001"  checked />
          <img src="../assets/img/di1.png">
        </label>
        <label for="option4">
          <input type="radio" id="option4" name="mode1" value = "002"  />
          <img src="../assets/img/di2.png">
        </label>
        <label for="option5">
          <input type="radio" id="option5" name="mode1" value = "003"  />
          <img src="../assets/img/di3.png">
        </label>
        <label for="option6">
          <input type="radio" id="option6" name="mode1" value = "004"  />
          <img src="../assets/img/di4.png">
        </label>
      </div>
      <div class="start-content">
        <img src="../assets/img/zidingyi.png" @click="showPage(4)" class="design">
      </div>
    </div>
    <div class="page page4" :class="{show:nowPage==4}">
      <div class="box-inside">
        <div class="positon-center back" @click="showPage(3)"><span>返回背景</span></div>
        <div class="positon-center canvas-box">
          <canvas id="canvas"></canvas>
          <canvas id="canvas1"></canvas>
        </div>
        <nav class="nav J_menu show">
          <div class="nav-box">
            <div class="item hair">
              <i></i>
              <span>发型</span>
            </div>
            <div class="item jacket">
              <i></i>
              <span>上衣</span>
            </div>
            <div class="item pants">
              <i></i>
              <span>下装</span>
            </div>
            <div class="item shoes">
              <i></i>
              <span>鞋子</span>
            </div>
            <div class="item object">
              <i></i>
              <span>装饰</span>
            </div>
            <div class="item eye">
              <i></i>
              <span>眼镜</span>
            </div>
            <div class="item hat">
              <i></i>
              <span>包包</span>
            </div>
          </div>
        </nav>
        <div class="nav J_list list">
          <ul class="nav-box nav-bg">
            <li class="hat">
              <div class="item hat">
                <i></i>
                <span>包包</span>
              </div>
              <div class="nav-scole">
                <div class="nav-scole-div">
                  <!--<span class="icon hat1"></span>-->
                  <!--<span class="icon hat2"></span>-->
                  <!--<span class="icon hat3"></span>-->
                  <!--<span class="icon hat4"></span>-->
                  <!--<span class="icon hat5"></span>-->
                  <!--<span class="icon hat6"></span>-->
                </div>
              </div>
            </li>
            <li class="eye">
              <div class="item eye">
                <i></i>
                <span>眼镜</span>
              </div>
              <div class="nav-scole">
                <div class="nav-scole-div">
                  <div class="cur-box cur">
                    <span class="icon eye1"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon eye2"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon eye3"></span>
                  </div>
                </div>
              </div>
            </li>
            <li class="hair" data-for="female">
              <div class="item hair">
                <i></i>
                <span>发型</span>
              </div>
              <div class="nav-scole">
                <div class="nav-scole-div">
                  <div class="cur-box cur">
                    <span class="icon femalehair1"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon femalehair2"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon femalehair3"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon femalehair4"></span>
                  </div>
                </div>
              </div>
            </li>
            <li class="jacket" data-for="female">
              <div class="item jacket">
                <i></i>
                <span>上衣</span>
              </div>
              <div class="nav-scole">
                <div class="nav-scole-div">
                  <div class="cur-box cur">
                    <span class="icon femalejacket1"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon femalejacket2"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon femalejacket3"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon femalejacket4"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon femalejacket5"></span>
                  </div>
                </div>
              </div>
            </li>
            <li class="pants" data-for="female">
              <div class="item pants">
                <i></i>
                <span>下装</span>
              </div>
              <div class="nav-scole">
                <div class="nav-scole-div">
                  <div class="cur-box cur">
                    <span class="icon femalepants1"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon femalepants2"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon femalepants3"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon femalepants4"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon femalepants5"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon femalepants6"></span>
                  </div>
                </div>
              </div>
            </li>
            <li class="shoes" data-for="female">
              <div class="item shoes">
                <i></i>
                <span>鞋子</span>
              </div>
              <div class="nav-scole">
                <div class="nav-scole-div">
                  <div class="cur-box cur">
                    <span class="icon femaleshoes1"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon femaleshoes2"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon femaleshoes3"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon femaleshoes4"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon femaleshoes5"></span>
                  </div>
                </div>
              </div>
            </li>
            <li class="object">
              <div class="item object">
                <i></i>
                <span>装饰</span>
              </div>
              <div class="nav-scole">
                <div class="nav-scole-div">
                  <div class="cur-box cur">
                    <span class="icon object1"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon object2"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon object3"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon object4"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon object5"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon object6"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon object7"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon object8"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon object9"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon object10"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon object11"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon object12"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon object13"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon object14"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon object15"></span>
                  </div>
                </div>
              </div>
            </li>
            <li class="hair" data-for="male">
              <div class="item hair">
                <i></i>
                <span>发型</span>
              </div>
              <div class="nav-scole">
                <div class="nav-scole-div">
                  <div class="cur-box cur">
                    <span class="icon malehair1 "></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon malehair2"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon malehair3"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon malehair4"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon malehair5"></span>
                  </div>
                </div>
              </div>
            </li>
            <li class="pants" data-for="male">
              <div class="item pants">
                <i></i>
                <span>下装</span>
              </div>
              <div class="nav-scole">
                <div class="nav-scole-div">
                  <div class="cur-box cur">
                    <span class="icon malepants1"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon malepants2"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon malepants3"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon malepants4"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon malepants5"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon malepants6"></span>
                  </div>
                </div>
              </div>
            </li>
            <li class="jacket" data-for="male">
              <div class="item jacket">
                <i></i>
                <span>上装</span>
              </div>
              <div class="nav-scole">
                <div class="nav-scole-div">
                  <div class="cur-box cur">
                    <span class="icon malejacket1"></span>
                  </div>
                  <div class="cur-box ">
                    <span class="icon malejacket2"></span>
                  </div>
                  <div class="cur-box ">
                    <span class="icon malejacket3"></span>
                  </div>
                  <div class="cur-box ">
                    <span class="icon malejacket4"></span>
                  </div>
                  <div class="cur-box ">
                    <span class="icon malejacket5"></span>
                  </div>
                  <div class="cur-box ">
                    <span class="icon malejacket6"></span>
                  </div>
                </div>
              </div>
            </li>
            <li class="shoes" data-for="male">
              <div class="item shoes">
                <i></i>
                <span class="yellow">鞋子</span>
              </div>
              <div class="nav-scole">
                <div class="nav-scole-div">
                  <div class="cur-box cur">
                    <span class="icon maleshoes1"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon maleshoes2"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon maleshoes3"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon maleshoes4"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon maleshoes5"></span>
                  </div>
                  <div class="cur-box">
                    <span class="icon maleshoes6"></span>
                  </div>
                </div>
              </div>
            </li>
          </ul>
          <span class="btn btn-small selec-close"  id="selectClose">返回分类</span>
        </div>
        <div class="positon-center foot-btns ml25">
          <span class="btn btn-small" @click="showPage(5)">生成海报</span>
        </div>
      </div>
    </div>
    <div class="page page5" :class="{show:nowPage==5}">
      <div class="box-inside">
        <div class="positon-center back" @click="showPage(4)"><span>返回编辑</span></div>
        <div class="imgbox">
          <div class="box-inside">
            <div class="box-inside-bg">
              <img src="../assets/img/haibao.png" class="display head-img J_head_display">
            </div>
          </div>
        </div>
        <div class="positon-center foot-btns">
          <span class="btn">长按保存</span>
          <span class="btn" onclick="alert('请点击右上角微信分享');">分享海报</span>
        </div>
      </div>
    </div>
    <audio id="bgmusic" src="../assets/music/yinyue.mp3" style="display: none" autoplay preload loop></audio>
  </div>
</template>

<script>
  import wx from 'weixin-js-sdk';
  export default {
    name: 'index',
    data () {
      return {
        nowPage:0
      }
    },
    mounted(){
    },
    methods: {
      showPage(index){
        this.nowPage=index
      },
    }
  }
</script>
