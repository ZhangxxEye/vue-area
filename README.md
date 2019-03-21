# vue-area
移动端选择地址组件
![](//cdn.51talk.com/apollo/images/6ec0e8ad944157a52e0368657ec84bf2.png//cdn.51talk.com/apollo/images/f2887eafaa0c6386a85ef838c5936558.png)
## install
NPM
```
npm install @nat/vue-area
```
## 用法
```
 <div id="project-features">
        <h1 class="title">地区</h1>
        <div class="features">
            <vue-area :area-ids="areaIds" :area-list="areaList" @selected="select"></vue-area>
        </div>
    </div>
```
```
<script>
    import area from '@nat/vue-area';

    export default {
        components: {
            area
        }
    };
</script>
```
## API
#### props
属性 | 说明 | 类型 | 默认值
---|---|---|---
areaList | 地区列表(数据格式下文给出) | Array | []
areaIds | 初始化选择的地区值(以逗号分隔的id值，例如："110000,110100,110101") | String | []
#### areaList的数据格式
```
[
    {
      "id": "110000",
      "name": "北京",
      "pid": "0",
      "subcat": [
        {
          "id": "110100",
          "name": "北京市",
          "pid": "110000",
          "subcat": [
            {
              "id": "110101",
              "name": "东城区",
              "pid": "110100"
            },
            {
              "id": "110102",
              "name": "西城区",
              "pid": "110100"
            }
          ]
        }
      ]
    }
  ]
```
#### event
事件名 | 说明 | 参数值 | 类型
---|---|---
selected | 选择的省市区| 选择的省市区 | Object
#### selected事件返回的参数的数据类型
```
{
    city: { // 市
        id: '00000',
        name: '天津市'
    },
    pro: {//省
        id: '00000',
        name: '天津'
    },
    dis: {//区
        id: '00000',
        name: '和平区'
    }
}
```
## 启动
```
npm run dev
```
## 编译
```
npm run build-lib
```
