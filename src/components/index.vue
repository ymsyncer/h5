<template>
  <div class="wrap">
    <div class="loading" id="loading"></div>
    <img :src="musicImg" class="music" @click="playPause">
    <div class="page page0" :class="{show:nowPage==0}">
      <img :src="start" class="start-img">
      <div class="start-content">
        <a class="btn" @click="showPage(1)">立即开始</a>
      </div>
    </div>
    <div class="page page1" :class="{show:nowPage==1}">
      <div class="upload-content">
        <div class="upload-box" id="crop_result">
          <img :src="camaraImg"/>
        </div>
      </div>
      <div class="upload-footer clearfix">
        <div class="con-3">
          <a @click="choose_form_album" class="file_input file_input1">
            <img src="../assets/img/shangchaun.png">
          </a>
        </div>
        <div class="con-4">
          <a @click="choose_form_camera" class="file_input">
            <img src="../assets/img/paizhao.png">
          </a>
        </div>
        <div class="con-3">
          <div class="haibao-bg-head upload-btn" @click="upload">选择性别</div>
        </div>
      </div>
    </div>
    <div class="page page2" :class="{show:nowPage==2}">
      <div class="page2-content clearfix">
        <label for="option0">
          <img src="../assets/img/nan.png">
          <input type="radio" id="option0" v-model="sex" name="mode" value="1" checked/>
          <a class="btn">我是男生</a>
        </label>
        <label for="option1">
          <img src="../assets/img/nv.png">
          <input type="radio" id="option1" v-model="sex" name="mode" value="2"/>
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
          <input type="radio" id="option3" name="mode1" v-model="designType" value="bg1" checked/>
          <img src="../assets/img/di1.png">
        </label>
        <label for="option4">
          <input type="radio" id="option4" name="mode1" v-model="designType" value="bg2"/>
          <img src="../assets/img/di2.png">
        </label>
        <label for="option5">
          <input type="radio" id="option5" name="mode1" v-model="designType" value="bg3"/>
          <img src="../assets/img/di3.png">
        </label>
        <label for="option6">
          <input type="radio" id="option6" name="mode1" v-model="designType" value="bg4"/>
          <img src="../assets/img/di4.png">
        </label>
      </div>
      <div class="start-content">
        <img src="../assets/img/zidingyi.png" @click="goDesign" class="design">
      </div>
    </div>
    <div class="page page4" :class="{show:nowPage==4}">
      <div class="box-inside">
        <div class="positon-center back" @click="showPage(3)"><span>返回背景</span></div>
        <div class="positon-center canvas-box">
          <div class="people" v-if="sex==1">
            <img :src="maleBody.body">
            <img :src="maleBody.img"/>
            <img :src="maleBody.malehair">
            <img :src="maleBody.malepants">
            <img :src="maleBody.malejacket">
            <img :src="maleBody.maleshoes">
            <img :src="maleBody.maleobject">
            <img :src="maleBody.eye">
          </div>
          <div class="people" v-if="sex==2">
            <img :src="femaleBody.body">
            <img :src="femaleBody.img"/>
            <img :src="femaleBody.femalehair">
            <img :src="femaleBody.femalepants">
            <img :src="femaleBody.femalejacket">
            <img :src="femaleBody.femaleshoes">
            <img :src="femaleBody.femaleobject">
          </div>
          <canvas id="canvas" style="opacity: 0;"></canvas>
        </div>
        <nav class="nav" :class="{show:!isIcon}">
          <div class="nav-box">
            <div v-if="sex==1" v-for=" type in types" class="item" :class="type.class">
              <i @click="selectDetail(type)"></i>
              <span>{{type.name}}</span>
            </div>
            <div v-if="sex==2" v-for=" type in feTypes" class="item" :class="type.class">
              <i @click="selectDetail(type)"></i>
              <span>{{type.name}}</span>
            </div>
          </div>
        </nav>
        <div class="nav" :class="{show:isIcon}">
          <ul class="nav-box nav-bg">
            <li :class="{show:nowType=='eye'}">
              <div class="item eye">
                <i></i>
                <span>眼镜</span>
              </div>
              <div class="nav-scole">
                <div class="nav-scole-div">
                  <div v-for="i in 2" @click="change('eye',i)" class="cur-box" :class="{cur:i==eyeIndex}">
                    <span class="icon" :class="'eye'+i"></span>
                  </div>
                </div>
              </div>
            </li>
            <li :class="{show:nowType=='female-hair'}">
              <div class="item hair">
                <i></i>
                <span>发型</span>
              </div>
              <div class="nav-scole">
                <div class="nav-scole-div">
                  <div @click="change('femalehair',i)"
                       v-for="i in 12"
                       class="cur-box"
                       :class="{cur:i==femalehairIndex}">
                    <span class="icon" :class="'femalehair'+i"></span>
                  </div>
                </div>
              </div>
            </li>
            <li :class="{show:nowType=='female-jacket'}">
              <div class="item jacket">
                <i></i>
                <span>上衣</span>
              </div>
              <div class="nav-scole">
                <div class="nav-scole-div">
                  <div @click="change('femalejacket',i)"
                       v-for="i in 6"
                       class="cur-box"
                       :class="{cur:i==femalejacketIndex}">
                    <span class="icon" :class="'femalejacket'+i"></span>
                  </div>
                </div>
              </div>
            </li>
            <li :class="{show:nowType=='female-pants'}">
              <div class="item pants">
                <i></i>
                <span>下装</span>
              </div>
              <div class="nav-scole">
                <div class="nav-scole-div">
                  <div @click="change('femalepants',i)"
                       v-for="i in 6"
                       class="cur-box"
                       :class="{cur:i==femalepantsIndex}">
                    <span class="icon" :class="'femalepants'+i"></span>
                  </div>
                </div>
              </div>
            </li>
            <li :class="{show:nowType=='female-shoes'}">
              <div class="item shoes">
                <i></i>
                <span>鞋子</span>
              </div>
              <div class="nav-scole">
                <div class="nav-scole-div">
                  <div @click="change('femaleshoes',i)"
                       v-for="i in 6"
                       class="cur-box"
                       :class="{cur:i==femaleshoesIndex}">
                    <span class="icon" :class="'femaleshoes'+i"></span>
                  </div>
                </div>
              </div>
            </li>
            <li :class="{show:nowType=='object'}">
              <div class="item object">
                <i></i>
                <span>装饰</span>
              </div>
              <div class="nav-scole">
                <div class="nav-scole-div">
                  <div v-if="sex==1" v-for="i in 9"  @click="change('maleobject',i)" class="cur-box" :class="{cur:i==maleobjectIndex}">
                    <span class="icon" :class="'maleobject'+i"></span>
                  </div>
                  <div v-if="sex==2" v-for="i in 7" @click="change('femaleobject',i)" class="cur-box" :class="{cur:i==femaleobjectIndex}">
                    <span class="icon" :class="'femaleobject'+i"></span>
                  </div>
                </div>
              </div>
            </li>
            <li :class="{show:nowType=='male-hair'}">
              <div class="item hair">
                <i></i>
                <span>发型</span>
              </div>
              <div class="nav-scole">
                <div class="nav-scole-div">
                  <div @click="change('malehair',i)" v-for="i in 12" class="cur-box" :class="{cur:i==malehairIndex}">
                    <span class="icon" :class="'malehair'+i"></span>
                  </div>
                </div>
              </div>
            </li>
            <li :class="{show:nowType=='male-pants'}">
              <div class="item pants">
                <i></i>
                <span>下装</span>
              </div>
              <div class="nav-scole">
                <div class="nav-scole-div">
                  <div @click="change('malepants',i)" v-for="i in 7" class="cur-box" :class="{cur:i==malepantsIndex}">
                    <span class="icon" :class="'malepants'+i"></span>
                  </div>
                </div>
              </div>
            </li>
            <li :class="{show:nowType=='male-jacket'}">
              <div class="item jacket">
                <i></i>
                <span>上衣</span>
              </div>
              <div class="nav-scole">
                <div class="nav-scole-div">
                  <div @click="change('malejacket',i)" v-for="i in 7" class="cur-box" :class="{cur:i==malejacketIndex}">
                    <span class="icon" :class="'malejacket'+i"></span>
                  </div>
                </div>
              </div>
            </li>
            <li :class="{show:nowType=='male-shoes'}">
              <div class="item shoes">
                <i></i>
                <span class="yellow">鞋子</span>
              </div>
              <div class="nav-scole">
                <div class="nav-scole-div">
                  <div @click="change('maleshoes',i)" v-for="i in 7" class="cur-box" :class="{cur:i==maleshoesIndex}">
                    <span class="icon" :class="'maleshoes'+i"></span>
                  </div>
                </div>
              </div>
            </li>
          </ul>
          <span class="btn btn-small selec-close" @click="isIcon=false">返回分类</span>
        </div>
        <div class="positon-center foot-btns ml25">
          <span class="btn btn-small" @click="generate">生成海报</span>
        </div>
      </div>
    </div>
    <div class="page page5" :class="{show:nowPage==5}">
      <div class="box-inside">
        <div class="positon-center back" @click="showPage(4)"><span>返回编辑</span></div>
        <div class="imgbox">
          <div class="box-inside">
            <div class="box-inside-bg ">
              <img :src="downloadUrl" crossOrigin="anonymous" class="show">
            </div>
          </div>
        </div>
        <div class="positon-center foot-btns">
          <span class="btn">长按保存</span>
          <span class="btn">点击右上角分享</span>
        </div>
      </div>
    </div>
    <audio ref="player" :src="play_mp3_url" id="music" style="display: none" autoplay preload loop></audio>
  </div>
</template>
<script>
  import wx from 'weixin-js-sdk';
  import allPic from '@/assets/js/resourse'
  import axios from 'axios'
  var instance = axios.create({
    baseURL: 'http://118.190.76.178:8089/'
  });
  instance.interceptors.request.use(function (config) {
    document.getElementById("loading").style.display = "block";
    return config;
  }, function (error) {
    return Promise.reject(error);
  });
  instance.interceptors.response.use(function (response) {
    document.getElementById("loading").style.display = "none";
    return response;
  }, function (error) {
    document.getElementById("loading").style.display = "none";
    return Promise.reject(error);
  });
  function dataURLtoFile(dataurl, filename) {//将base64转换为文件
    var arr = dataurl.split(','), mime = arr[0].match(/:(.*?);/)[1],
        bstr = atob(arr[1]), n = bstr.length, u8arr = new Uint8Array(n);
    while(n--){
      u8arr[n] = bstr.charCodeAt(n);
    }
    return {
      type:mime,
      blob:new File([u8arr], filename, {type:mime})
    };
  }
  export default {
    name: 'index',
    data() {
      return {
        start:allPic.start,
        nowPage: 0,
        isIcon: false,
        sex: 1,
        isLoading: false,
        types: [
          { name: "发型", class: "hair" },
          { name: "上衣", class: "jacket" },
          { name: "下装", class: "pants" },
          { name: "鞋子", class: "shoes" },
          { name: "装饰", class: "object" },
          { name: "眼镜", class: "eye" }
        ],
        feTypes: [
          { name: "发型", class: "hair" },
          { name: "上衣", class: "jacket" },
          { name: "下装", class: "pants" },
          { name: "鞋子", class: "shoes" },
          { name: "装饰", class: "object" }
        ],
        hairClass: [],
        nowType: "",
        canvas: "",
        context: "",
        downloadUrl: "",
        W: "",
        H: "",
        maleBody: {
          body: allPic.malebody,
          img:"",
          malepants: allPic.malepants.malepants1,
          maleshoes: allPic.maleshoes.maleshoes1,
          malejacket: allPic.malejacket.malejacket1,
          eye: "",
          malehair: allPic.malehair.malehair1,
          maleobject: allPic.maleobject.maleobject1,
        },
        femaleBody: {
          body: allPic.femalebody,
          img: "",
          femalepants: allPic.femalepants.femalepants1,
          femaleshoes: allPic.femaleshoes.femaleshoes1,
          femalejacket: allPic.femalejacket.femalejacket1,
          femalehair: allPic.femalehair.femalehair1,
          femaleobject: allPic.femaleobject.femaleobject1
        },
        maleobject: allPic.maleobject,
        maleobjectIndex: 1,
        femaleobject:allPic.femaleobject,
        femaleobjectIndex: 1,
        eye: allPic.eye,
        eyeIndex: 0,
        malehair: allPic.malehair,
        malehairIndex: 1,
        maleshoes: allPic.maleshoes,
        maleshoesIndex: 1,
        malepants: allPic.malepants,
        malepantsIndex: 1,
        malejacket: allPic.malejacket,
        malejacketIndex: 1,
        femalehair: allPic.femalehair,
        femalehairIndex: 1,
        femaleshoes: allPic.femaleshoes,
        femaleshoesIndex: 1,
        femalepants: allPic.femalepants,
        femalepantsIndex: 1,
        femalejacket: allPic.femalejacket,
        femalejacketIndex: 1,
        haibaos: allPic.haibaos,
        selectBgs: allPic.selectBgs,
        designType: "bg1",
        peopleNum: 0,
        camaraImg: allPic.camaraImg,
        musicImg: allPic.playImg,
        play_mp3_url: allPic.music,
        picture:""
      }
    },
    mounted() {
      let rem = document.documentElement.clientWidth / 375 * 312.5 * 16 / 100;
      this.W = 7.5 * rem;
      this.H = 13.34 * rem;
      this.canvas = document.getElementById('canvas');
      this.context = this.canvas.getContext('2d');
      this.canvas.style.width = this.W + 'px';
      this.canvas.style.height = this.H + 'px';
      this.canvas.width = this.W * 2;
      this.canvas.height = this.H * 2;
      this.shareWX();
      let self = this;
      document.addEventListener("WeixinJSBridgeReady", function () {
        self.audioPlay();
      }, false);
    },
    methods: {
      goDesign() {
        let self = this;
        let formdata = new FormData();
        let template_url;
        if (self.sex == 1) {
          template_url="http://h5.1roadshow.com/static/male.png"
        }else {
          template_url="http://h5.1roadshow.com/static/female.png"
        }
        formdata.append('api_key', "WsMnjIMvwlgiFzOh_NghX_gU0ZLfGYiY");
        formdata.append('api_secret', "qZt6v9-qoJ33qfYd8iV2ujFTIgy6TLOE");
        formdata.append('template_url', template_url);
        formdata.append('merge_url',"http://123.207.161.92:8080/image-server/imageThumbnail?relUrl="+self.picture);
        instance.post("https://api-cn.faceplusplus.com/imagepp/v1/mergeface", formdata)
          .then((response) => {
            let formdata1 = new FormData();
            formdata1.append('base64', response.data.result);
            instance.post("http://123.207.161.92:8089/drees/covert", formdata1)
              .then((res) => {
                if (self.sex == 1) {
                  self.maleBody.img=res.data.returnValue
                } else {
                  self.femaleBody.img = res.data.returnValue
                }
                self.showPage(4)
              })
              .catch((err)=>{
                console.log(err);
              });
            // self.showPage(4)
          })
          .catch((err)=>{
            alert("未找到融合的图片");
            self.showPage(1)
          });
      },
      audioPlay() {
        this.play_mp3_url = allPic.music;
        this.$refs.player.play();
      },
      playPause() {
        if (this.$refs.player.paused) {
          this.$refs.player.play();
          this.musicImg = allPic.playImg
        } else {
          this.$refs.player.pause();
          this.musicImg = allPic.pauseImg
        }
      },
      shareWX() {
        var link = location.href;
        instance.get("http://118.190.76.178:8088/share/GETJSSDK",
          { params: { "url": link.split('#')[0] } }).then((val) => {
          let data = JSON.parse(val.data.returnValue);
          wx.config({
            debug: false,
            appId: data.appId,
            timestamp: data.timestamp,
            nonceStr: data.noncestr,
            signature: data.signature,
            jsApiList: [
              "onMenuShareTimeline",
              "onMenuShareAppMessage",
              "onMenuShareWeibo",
              "chooseImage",
              "getLocalImgData"
            ]
          });
          wx.error(function (res) {
            console.log(res);
          });
        });
        var title = "全民玩潮 你有多Skr？", desc = "快来测试你的潮值！";
        wx.ready(function (res) {
          wx.onMenuShareAppMessage({
            title: title,
            desc: desc,
            link: link,
            imgUrl: "http://h5.1roadshow.com/static/title.png",
            success: function (res) {
            },
            cancel: function (res) {
            }
          });
          wx.onMenuShareTimeline({
            title: title,
            link: link,
            imgUrl: "http://h5.1roadshow.com/static/title.png",
            success: function (res) {
            },
            cancel: function (res) {
            }
          });
          wx.onMenuShareWeibo({
            title: title,
            desc: desc,
            link: link,
            imgUrl: "http://h5.1roadshow.com/static/title.png",
            success: function () {
            },
            cancel: function () {
            }
          });
        });
      },
      getConfig(type) {
        let self = this;
        return {
          count: 1, // 默认9
          sizeType: ['original', 'compressed'], // 可以指定是原图还是压缩图，默认二者都有
          sourceType: [type], // 可以指定来源是相册还是相机，默认二者都有
          success: function (res) {
            wx.getLocalImgData({
              localId: res.localIds[0],
              success: function (res) {
                let localData = res.localData;
                if (localData.indexOf('data:image') != 0) {
                   localData = 'data:image/jpeg;base64,' +  localData
                }
                localData = localData.replace(/\r|\n/g, '').replace('data:image/jgp', 'data:image/jpeg');
                self.camaraImg = localData;
                self.upload(dataURLtoFile(localData,'123.jpg'));
              }
            });
          }
        }
      },
      choose_form_camera() {
        wx.chooseImage(this.getConfig('camera'))
      },
      choose_form_album() {
        wx.chooseImage(this.getConfig('album'))
      },
      upload(file) {
        let self = this;
        let fd = new FormData();
        fd.append('id', "WU_FILE_0");
        fd.append('name', "模型.png");
        fd.append('lastModifiedDate', new Date());
        fd.append('size', "16286");
        fd.append('type',file.type);
        fd.append('file', file.blob);
        if (file.blob == undefined) {
          self.showPage(2);
           return
        }
        instance.post("http://123.207.161.92:8080/image-server/uploadImage?mediaType=Picture&module=L", fd)
        .then((val) => {
          self.picture=val.data;
        })
        .catch((err)=>{
          console.log(err);
        });
        self.showPage(2);
      },
      drawCanvas() {
        let self = this, imgSrcArray = [];
        if (this.sex == 1) {
          if ((this.maleBody.img != "")) {
            imgSrcArray.push(this.maleBody.body,this.maleBody.img)
          }else {
            imgSrcArray.push(this.maleBody.body);
          }
          imgSrcArray.push(this.maleBody.malehair, this.maleBody.malepants, this.maleBody.malejacket, this.maleBody.maleobject, this.maleBody.maleshoes)
          if (this.maleBody.eye != "") {
            imgSrcArray.push(this.maleBody.eye)
          }
        } else {
          if ((this.femaleBody.img != "")) {
            imgSrcArray.push(this.femaleBody.body,this.femaleBody.img)
          }else {
            imgSrcArray.push(this.femaleBody.body);
          }
          imgSrcArray.push(this.femaleBody.femalehair, this.femaleBody.femalepants, this.femaleBody.femalejacket, this.femaleBody.femaleobject, this.femaleBody.femaleshoes);
        }
        let imglen = imgSrcArray.length;
        let drawimg = (function f(n) {
          if (n < imglen) {
            let img = new Image();
            img.crossOrigin = 'anonymous';
            img.onload = function () {
              self.context.drawImage(img, 0, 0, self.canvas.width * 0.54, self.canvas.height * 0.68, self.canvas.width * 0.25, self.canvas.height * 0.1, self.canvas.width * 0.54 * 0.91, self.canvas.height * 0.68 * 0.91);
              self.context.restore();
              f(n + 1);
            };
            img.src = imgSrcArray[n];
          } else {
            self.downloadUrl = self.canvas.toDataURL("image/jpeg");
            self.showPage(5)
          }
        })(0);
      },
      drawBg() {
        let self = this;
        self.context.fillStyle = '#FFFFFF';
        self.context.fillRect(0, 0, this.W * 2, this.H * 2);
        let img = new Image();
        img.src = self.haibaos[Math.floor((Math.random() * self.haibaos.length))];
        img.onload = function () {
          self.context.save();
          self.context.drawImage(img, 0, 0, self.canvas.width, self.canvas.height, 100, 0, self.canvas.width, self.canvas.height);
          self.context.restore();
          self.drawSelectBg();
        };
        let imgBg = new Image();
        imgBg.crossOrigin = "anonymous";
        imgBg.src = allPic.haibaoBg;
        imgBg.onload = function () {
          self.context.save();
          self.context.drawImage(imgBg, 0, 0, self.canvas.width, self.canvas.height * 0.99);
          self.context.font = "30px HYYaKuHeiJ";
          self.context.fillStyle = "#ff0092";
          let score = Math.floor(Math.random() * (100 - 78)) + 78;
          self.context.fillText(score, self.canvas.width * 0.58, self.canvas.height * 0.915);
          self.context.font = "25px HYYaKuHeiJ";
          self.context.fillStyle = "#ababac";
          self.context.fillText("当 然 啦,你 还 有 " + self.peopleNum + " 个 手 下 败 将！", self.canvas.width * 0.08, self.canvas.height * 0.955);
        }
      },
      drawSelectBg() {
        let self = this, imgUrl = new Image();
        imgUrl.crossOrigin = "anonymous";
        imgUrl.src = self.selectBgs[self.designType];
        imgUrl.onload = function () {
          self.context.save();
          self.context.drawImage(imgUrl, 0, 0, self.canvas.width, self.canvas.height);
          self.context.restore();
          self.drawCanvas()
        };
      },
      generate() {
        let self = this;
        self.context.clearRect(0, 0, this.W * 2, this.H * 2);
        instance.get("drees/insert").then((res) => {
          self.peopleNum = res.data.returnValue;
          self.drawBg();
        })
      },
      change(val, i) {
        this[val + "Index"] = i;
        if (this.sex == 1) {
          this.maleBody[val] = this[val][val + i];
        } else {
          this.femaleBody[val] = this[val][val + i];
        }
      },
      showPage(index) {
        this.nowPage = index;
        this.isIcon = false
      },
      selectDetail(type) {
        if (['eye', 'object'].indexOf(type.class) != -1) {
          this.nowType = type.class;
        } else {
          if (this.sex == 1) {
            this.nowType = "male" + "-" + type.class;
          } else {
            this.nowType = "female" + "-" + type.class;
          }
        }

        this.isIcon = true
      }
    },
    watch: {
      play_mp3_url() {
        let self = this;
        self.$nextTick(() => {
          self.$refs.player.play();
        })
      }
    }
  }
</script>
