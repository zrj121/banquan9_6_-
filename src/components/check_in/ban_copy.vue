<template>
<div>
    <!--作品分类类型 -->
    <div class="thickness" v-show="isthickness">
            <p class="thickness_name">专业分类<img @click="cl_img" src="../../static/images/guanbi.png"/> </p>
            <p class="thickness_fl">
                <span :disabled="noMore" :class=" choose_co ?'th_xz':''" >{{flname}}</span>
                <span :class=" choose_co ?'':'th_xz'" @click="clickfl">请选择</span>
            </p>
            <div class="thickness_m">
             <p v-for="(item, index ) in listType" :key="index" @click="click_in(index)">{{item.name}}</p>
          
            </div>
        </div>

    <!-- 以上是作品类型分类 -->

<div class="ban_copy ban_detail">
    <v-touch v-on:swiperight="onSwiperRight" id="swiper_id">
        <span class="icon_img_1" @click="get_swiper" >
        <img src="../../static/images/img_info.png" alt="">
         </span>
      </v-touch> 
     
    
    
   <div class="ban_content_1">
         <div class="other">
        <label for="name">作品名称 :&nbsp;<input type="text" id="name" style=" height: 17px; width:125px;margin-top:.6rem" placeholder="填写" v-model="art_name" ></label>
       <div >作品编码 :&nbsp;<span style=" height: 1.266667rem; width: 10rem;margin-top:.6rem"></span></div>

         <div class="flex-h flex-a-c " style="margin-top:19px; ">   
        <div class="flex-h flex-a-c ">创作性质:&nbsp;  原创</div>
        <div class="flex-h flex-a-c " style="margin-left:50px">作品分类 :&nbsp; 美术</div>
        </div>
         <div class="flex-h flex-a-c " style=" justify-content: space-between">   
        <div class="flex-h flex-a-c "  > 
          <label for="name_name">存证者 : &nbsp;<input type="text" style=" height: 17px; width:53px;margin-top:.6rem" placeholder="填写" v-model="art_person" id="name_name">
          </label>
          <div style="margin-left:28px;">存证时间 : &nbsp;<span style=" height: 17px; width: 53px;margin-top:.6rem"></span></div>
          </div>
       
        </div>    
             <div  style="margin-top:11px;">
             <p >作品描述</p> 
             <div class="detail_zuo">
                  <div class="w flex-h b-b m-t flex-a-c lei_class_div"  style="margin:2px 0 0 8px;z-index:999" >
                 <div >专业分类 ：&nbsp;</div>
                <div class="lei_class bottom-1" @click='goodsfl'>
                    <p class=" c2 " v-if='goodt_n' style="width: 6rem;" >{{goodt_n}}</p>
                    <p class=" c2 " v-else style="width:6rem;">请选择</p>
                </div>
                 
            </div >
            <span  class="text" id="text_text">填写（120字以内）</span>
             <textarea name="" style="text-indent:10rem; height:98px; padding:0;color:#000;background:#F1EFEB" @click="text_change" v-model="art_text">
  
             </textarea>
             </div>    

             </div>
           

      </div>

    </div>  
   <!-- 以下代码是传图片的 -->
       <div class="top">
        <v-touch v-on:swiperight="onSwiperRight_img" id="swiper_id_img">
        <span class="icon_img_2" @click="get_swiper_img" >
        <img src="../../static/images/upload_img_1.png" alt="">
         </span>
      </v-touch> 
     
      <div class="upload_img">
        <!-- 主图和附图 -->
        
         <div class="upload_master " style="border-bottom: .0625rem solid #BFBFBF;border-right: .0625rem solid #BFBFBF;" @click="show_list('one')">
         <div class="no_img" v-show="!url_list_one">
         <img src="../../static/images/add_img.png" alt="">
         </div>

         <div class="has_img" v-show="url_list_one">
            <img :src="url_list_one" alt="" id="img_one"> 
         </div>
         </div>

    <!-- <div class="has_img">
            <img :src="url_list_one"> 
         </div>
         </div> -->


         <div class="upload_branch">
          <div class="upload_img_two item" style="border-bottom: .0625rem solid #BFBFBF;" @click="show_img('two')">
         <div class="no_img" v-show="!url_list_two">
         <img src="../../static/images/add_img.png" alt="">
         </div>
          <div class="has_img" v-show="url_list_two">
            <img :src="url_list_two" alt="" id="img_two"> 
         </div>
         </div>
          <div class="upload_img_three item" style="border-right: .0625rem solid #BFBFBF;" @click="show_img_two('three')">
         <div class="no_img"  v-show="!url_list_three">
         <img src="../../static/images/add_img.png" alt="">
         </div>
          <div class="has_img" v-show="url_list_three">
            <img :src="url_list_three" alt="" id="img_three"> 
         </div>
         </div>
             <div class="upload_img_four item" @click="show_img_three('four')">
         <div class="no_img" v-show="!url_list_four">
         <img src="../../static/images/add_img.png" alt="">
         </div>
          <div class="has_img" v-show="url_list_four">
            <img :src="url_list_four" alt="" id="img_four"> 
         </div>
         </div>
    </div>
       

    </div> 

    </div> 
      
  </div>   
 
   <div class="agree t-c c1">
       <div>
       <label for="classify"><input type="checkbox" id="classify" class="__input" style="margin-right:14px"> </label>
       <span>已阅读同意</span>
        <span style="font-size:14px;color:#4A8ADA" @click="go_user_polo">《版权协议》</span>
            <div class="submit-btn-1" style="margin: 11px auto 0" @click="art_btn">
               上传认证
            </div>
            </div>
    </div> 
    <!-- 点击upload上传作品 -->
        <!-- <upload v-if="show_select_upload" @close_upload ="close"></upload> -->
         <!-- 切换子路由 -->
         <!-- <router-view class="child_view"></router-view>   -->
        <!-- 1.上传照相机的input -->
         <input type="file" class="hide file" accept="image/*" @change="upload_img">
</div>
 
     
</template>

<script>

import upload from '../asset/upload/upload.vue';
import util from '../../libs/util'

export default {
     mounted(){
        // let url_list = this.$route.query.url;
        // let num = this.$route.query.num;
        // if(num){
        //     let url = this.$route.query.url
        //     this.url_list.five = url
        // }
        //    url_list =JSON.parse(url_list)
        //    this.url_list = url_list  
      },
      data(){
        return{
         area_address: null,
         show_select_address: false,
         show_out:false,
         show_select_upload:false, //上传作品默认是隐藏的 
         url_list:[], //存放图片路径的对象，存证的路径
         num:null, 
        //作品分类
         isthickness:false,
         flname:"一级分类", 
         listType:[], //作品分类列表
         goodsType:[],
         goodt_n:null, //专业类型
         choose_co:false, //默认

        // 储存的信息
         art_name:null, // 存证作品名
         art_person:null, //存证者
         art_text:null,// 存证的描述
         url_list_one:null, //上传图片一
         url_list_two:null,//上传图片二
         url_list_three:null,//上传图片三
         url_list_four:null,//上传图片四
         url_list_five:null,//上传图片五
         num:null,//传入参数num
        //  arr:[],
        
        }
    },
     components: {
           
            upload:upload
        },
        created(){
              var that = this
        },
    methods:{
          
            show_list(num){
                // debugger
                this.num = 'one';
                const file = document.querySelector(".file");
                file.click(); 
               
            },
            show_img(num){
                const file = document.querySelector(".file");
                file.click(); 
                this.num = num;
            },
            show_img_two(num){
                const file = document.querySelector(".file");
                file.click(); 
                this.num = num;
            },
            show_img_three(num){
                const file = document.querySelector(".file");
                file.click(); 
                this.num = num;
                     
            },
            show_img_four(num){
              const file = document.querySelector(".file");
              file.click(); 
              this.num = num;      
            },
            upload_img(e) {
                // debugger
                var num = this.num;
                let formData = new FormData();
                formData.append('file', e.target.files[0]);
                formData.append('type', 'test');
                // 发送异步请求，把formData发送异步请求
                this.util.ajax.post("/admin/authCopyright/upload.do", formData).then(e => {
                    // debugger
                    
                     if(num == 'one'){
                        this.url_list_one = e.path;  
                        this.url_list.push(this.url_list_one);
                        

                     }else if(num =='two'){
                        this.url_list_two = e.path
                        // this.arr.add(e.path);
                        this.url_list.push(this.url_list_two);


                     }else if(num =='three'){
                        this.url_list_three = e.path
                        this.url_list.push(this.url_list_three);

                     }else if(num == 'four'){
                         this.url_list_four = e.path
                         this.url_list.push(this.url_list_four);
         
                     }
                    //  else if(num == 'five'){
                    //      this.url_list_five = e.path
                    //      this.url_list.push(this.url_list_five);
                    // //  this.show_img_four(e.path);  
                    // }                     
                }).catch()
            },

            close(){
               this.show_select_upload =false;
            },
            // 滑动的操作
              onSwiperRight(){
                //2.实现向右滑动  
                $("#swiper_id>span").animate({
                    right:"-6.466667rem"
                }, 800);
            },
            // 点击滑动
            get_swiper(){
                // 1.点击实现向右滑动
                $('#swiper_id>span').animate({
                    right:"-6.466667rem"
                }, 800);
            },

            // 图片滑动条
              onSwiperRight_img(){
                //2.实现向右滑动  
                $("#swiper_id_img>span").animate({
                    right:"-6.466667rem"
                }, 800);
            },
            // 点击滑动
            get_swiper_img(){
                // 1.点击实现向右滑动
                $('#swiper_id_img>span').animate({
                    right:"-6.466667rem"
                }, 800);
            },
            // 打开作品分类弹出层
            noMore(){
                this.choose_co =false
            },
             clickfl(){
            //    this.choose_co =false
                // if(e==1){
                //     this.choose_co = true;
                //     this.clickfl(2)
                //     this.choose_co =false
                    

                // }
            
          },
           click_in(e){
            if(this.choose_co){
                this.listType = this.goodsType[e].list;
                this.flname = this.goodsType[e].name;
                this.categories = this.goodsType[e].id;
                this.choose_co = false;
            }else{
                this.smallclass =  this.listType[e].id;
                this.goodt_n = this.listType[e].name;
                this.isthickness = false;
            }
        },
        cl_img(){
            this.isthickness = false;
        },
         goodsfl(){
            // 这里是选择地址
            this.isthickness = true;
            this.flname = "请选择";
            this.choose_co = true;                       
         let info= [
            {id: 1, name: '艺术设计类', list: [
            {id: 1, name: '家具设计'},
            {id: 2, name: '厨具用品'},
            {id: 3, name: '灯饰灯具'},
            {id: 4, name: '家居软装'},
            {id: 5, name: '家居配饰'},
            {id: 6, name: '男装'},
            {id: 7, name: '女装'},
            {id: 8, name: '童装'},
            {id: 9, name: '老年装'},
            {id: 10, name: '配饰'},
            {id: 11, name: '鞋帽'},
            {id: 12, name: '箱包'},
            {id: 13, name: '珠宝首饰'},
            {id: 14, name: '交通运输'},
            {id: 15, name: '办公用品'},
            {id: 16, name: '家用电器'},
            {id: 17, name: '数码电子'},
            {id: 18, name: '智能设备'},
            {id: 19, name: '室内设计'},
            {id: 20, name: '园林规划'},
            {id: 21, name: '建筑设计'},
            {id: 22, name: '包装'},
            {id: 23, name: '纸本'},
            {id: 24, name: '动漫'},
            {id: 25, name: '影视'},
            {id: 26, name: '商业'},
            {id: 27, name: '其它'},
            ]},
            {id: 2, name: '造型艺术类', list: [
            {id: 28, name: '国画'},
            {id: 29, name: '油画'},
            {id: 30, name: '版画'},
            {id: 31, name: '壁画'},
            {id: 32, name: '水彩'},
            {id: 33, name: '插画'},
            {id: 34, name: '浮雕'},
            {id: 35, name: '圆雕'},
            {id: 36, name: '环境雕塑'},
            {id: 37, name: '装置'},
            {id: 38, name: '书法'},
            {id: 39, name: '篆刻'},
            {id: 40, name: '碑帖'},
            {id: 41, name: '塑作类'},
            {id: 42, name: '编织类'},
            {id: 43, name: '剪刻类'},
            {id: 44, name: '印染类'},
            {id: 45, name: '书画'},
            {id: 46, name: '瓷杂'},
            {id: 47, name: '珠宝'},
            {id: 48, name: '文玩'},
            {id: 49, name: '家具'},
            {id: 50, name: '其它'},
            ]}
        ]
        this.goodsType =info;
        this.listType = this.goodsType;             
        },
        text_change(){
            $('#text_text').hide()
        },
        //提交存证信息
           art_btn(){
               
           let name =  this.art_name
           let auth_name = this.art_person
           let type_name = this.goodt_n
           let production_note = this.art_text
           let url = this.url_list
           let url_str = '';
         
           if(url[0] !=null){
               url_str +=url[0]+",";
           }
           if(url[1] !=null){
               url_str +=url[1]+",";
           }
           if(url[2] !=null){
               url_str +=url[2]+",";
           }
           if(url[3] !=null){
               url_str +=url[3]+",";
           }
         console.log("url_str0000:"+url_str)
           var url01 = url_str.substring(url_str.length - 1, url_str.length);
          console.log("url01111："+url01)
       if(url01 == ',') {
         url =  url_str.substring(0,url_str.length - 1)
       }else{
           url = url_str;
       }
//    console.log("我需要的url"+url)



          //获取是否点击 阅读协议
            let result = $("#classify").is(":checked");
              
           if(name == null){
               this.Toast('请输入作品名称')
               return false
           }else if(auth_name == null ){
               this.Toast('请输入存证者')
               return false
           }else if(type_name == null){
             this.Toast('请选择专业类型')
             return false 

           }else if(production_note == null){
             this.Toast('请输入作品描述')
             return false
           }else if(!result){
             this.Toast('请阅读用户协议')
             return false
           }else{
               
            // 提交存证数据//
             let _p ={
              name,
              auth_name,
              type_name,
              production_note,
              url,
              
             }
             let paramStr = JSON.stringify(_p); 
             let _np = {
                 paramStr:paramStr,
                 type:1
             }//
             debugger
             this.util.ajax.post('/admin/copyrightTemp/save.do',_np).then(e=>{  
               console.log(e.code);
                     if(e.code ==200){
                        this.$router.push('/secret?number='+name)
                     }
              })
              
           }            
           },
           go_user_polo(){
                 this.$router.push('polo')
           }
            }
}
</script>
<style lang="less">
  @import 'ban_copy.less';

</style>


