# 小程序多列表的显示和隐藏


> 今天在项目碰到一个问题，之前在项目首页实现单列表的显示和隐藏，通过wx:if判断就可实现，现在要实现多列表的单项显示和隐藏功能应该如何实现呢？如果还用wx:if实现的话会出现点击一个列表项，多个列表同时显示和隐藏，明显不适合功能需求，然后简单地查了资料也没发现有类似的功能，最后思考一番后，慢慢地理清了思路...

##### 效果图：

![显示和隐藏.gif](http://upload-images.jianshu.io/upload_images/4041074-9d66bfd6440d7bb6.gif?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


###### 实现思路：
- 实现单个列表的显示和隐藏应该使用唯一元素让程序知道你应该显示和隐藏哪个列表项，可以用数据的id；
- css中定义一个hidden{display：none}控制显示和隐藏，然后通过三元运算符来判断；
- wxml定义一个点击事件来动态修改这个列表项的变量值。

###### 功能实现：
好了，思路有了，就开始按照思路来用代码验证。果不其然，使用代码实现之后，发现自己的思路还是没错的。此功能点也可以应用到其它类似的列表的显示和隐藏中。

###### 示例代码：
```
<!--pages/myOrder/myOrder.wxml-->
<view class='container'>
  <!-- 订单列表 -->
  <block wx:for-items="{{carInfoData}}">
    <view class='card  b-shadow' bindtap='toggleBtn' id="{{item.id}}">
      <view class='nearCard-fl'>
        <image src='{{item.imgurl}}'></image>
      </view>
      <view class='nearCard-fr'>
        <view>日期：
          <text class='c-green'>{{item.useDate}}</text>
        </view>
        <view>车型：
          <text class='c-green'>{{item.cx}}</text>
        </view>
        <view>时长：
          <text class='c-green'>{{item.time}}</text>
        </view>
        <view>费用：
          <text class='c-green'>{{item.feiyong}}</text>
        </view>
      </view>
      <view class='down clearfix {{uhide==item.id?"":"hidden"}}'>
        <view class='ml30'>启用时间：2018.01.01 11:33</view>
        <view class='ml30'>结束时间：2018.01.01 11:33</view>
        <view class='ml30'>租赁地区：舟山市桃花岛景区海湾浪琴</view>
        <view class='feedBack'>意见反馈</view>
      </view>
    </view>
  </block>
</view>
```
```
// pages/myOrder/myOrder.js
Page({

  /**
   * 页面的初始数据
   */
  data: {
    uhide: 0
  },

  /**
   * 生命周期函数--监听页面加载
   */
  onLoad: function (options) {
    var that = this;

    var data = {
      "datas": [
        {
          "id": 1,
          "imgurl": "../../images/car.png",
          "useDate": "2017-12-22",
          "cx": "奇瑞EQ1",
          "time": "1小时",
          "feiyong": "20元"
        },
        {
          "id": 2,
          "imgurl": "../../images/car.png",
          "useDate": "2017-12-22",
          "cx": "奇瑞EQ1",
          "time": "1小时",
          "feiyong": "20元"
        },
        {
          "id": 3,
          "imgurl": "../../images/car.png",
          "useDate": "2017-12-22",
          "cx": "奇瑞EQ1",
          "time": "1小时",
          "feiyong": "20元"
        },
        {
          "id": 4,
          "imgurl": "../../images/car.png",
          "useDate": "2017-12-22",
          "cx": "奇瑞EQ1",
          "time": "1小时",
          "feiyong": "20元"
        }
      ]
    };
    //console.log(data.datas);
    //设置车辆展示信息
    that.setData({
      carInfoData: data.datas
    })
  },

  //点击切换隐藏和显示
  toggleBtn: function (event) { 
    var that = this;
    var toggleBtnVal = that.data.uhide;
    var itemId = event.currentTarget.id; 
    if (toggleBtnVal == itemId) {
      that.setData({
        uhide: 0
      })
    } else {
      that.setData({
        uhide: itemId
      })
    } 
  }
})
```
