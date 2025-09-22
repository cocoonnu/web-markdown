# 开发记录

## 项目发布

发版流程：腾讯云 - 控制台 - 对象存储 - 存储桶路径找到对应的桶和项目目录，然后将打包之后 build 文件夹里面的所有文件上传即可，最后进入腾讯云 - 控制台 - 内容分发网络CDN - 刷新预热 - 目录刷新，然后提交，进入网站查看是否部署成功

```
灰豚数据测试环境
桶：dy-test-1255497916
命令：cnpm run build
位置：app/
http://dywebtest.huitun.com/
https://dywebtest.huitun.com/
```

```
灰豚精选测试环境
桶：douyin-jx-1255497916
命令：yarn testBuild
位置：test/
http://jx.huitun.com
https://jx.huitun.com
```

```
灰豚精选线上环境
桶：douyin-jx-1255497916
命令：yarn build
位置：根目录
http://jx.huitun.com
https://jx.huitun.com
```



## 项目安排
**灰豚精选**

- [x] 直播间详情页增加单个商品添加橱窗交互
- [x] 直播间详情页增加商品批量添加橱窗交互
- [x] 达人详情页增加单个商品添加橱窗交互
- [x] 达人详情页增加商品批量添加橱窗交互
- [x] 添加橱窗之后成功、失败弹窗逻辑
- [x] 添加橱窗、批量添加橱窗埋点（可能是后端）
- [x] 升佣成功提示弹窗
- [x] 授权成功弹窗提示
- [x] 达人详情页商品列表全选交互
- [x] 达人详情添加绑定品牌



**灰豚数据**



**独立站**



**直播后台**

- [x] 行业洞察新页面



**灰豚数据小程序**



**测试待办**

- [ ] 行业洞察可选类目并多选



**接口文档**



## 项目开发

**权限判断以及弹窗提示，最详细用户权限获取：useLevelInfo**

```js
const isProfessional =
  currentUser.vipLevel >= 5 && !currentUser.tryOutUser && !currentUser.user149;
if (isProfessional) {
  ......
} else {
  hintModal('该功能仅限于企业版及以上版本会员使用，', 7);
}
```

```js
const isPersonal = currentUser.vipLevel >= 5 && !currentUser.tryOutUser
if (isPersonal) {
  ......
} else {
  hintModal('该功能仅限于个人版及以上版本会员使用，', 5);
}
```

```js
if (currentUser.vipLevel === 10) {
  ......
} else {
  hintModal('该功能仅限品牌版会员使用，', 10);
}
```



**配置带有背景图的 Modal**

有两种效果，一种是 Modal 背景透明然后直接用一个图片进行占位，如果有其他内容则使用绝对定位；另一种是将 Modal 的 body 添加背景图片，以此实现效果样式；

效果一实例组件：src/components/HeightCosRatioModal/index.jsx，缺点：当图片还没有加载出来时，会导致文字飘了一下

效果二实例组件：src/components/DyAuthSuccess/index.jsx、src/components/BenefitsListModal/BenefitsListByUserModal.jsx，缺点：看交互图是否支持







