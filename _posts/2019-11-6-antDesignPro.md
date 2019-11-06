---
layout:     post                  #不要管他
title:      ant Design Pro     #标题
subtitle:   ant Design  Pro V2            #别名,简介,标题下面的那一行字
date:       2019-11-6            #发表时间
author:     Zhaolai                    #作者
header-img: img/post-bg-rwd.jpg   #背景图片
catalog: true                     #导航目录,不要管他
original: true                    #是否原创申明
tags:                             #标签,可以有多个
    - ant Design Pro
    - ant Design
---

## 安装

采用git克隆方式, 可以在当前文件夹新建一个文件夹用于存放

`git clone --depth=1 https://github.com/ant-design/ant-design-pro.git 新建文件名 -b v2`

进入文件夹后运行`npm install`安装环境

## 目录

#### config

router.config.js 设置路由

```js
export default [
    {
        path: '/user',
        component: '../layouts/UserLayout',
        // 权限
        authority: ['admin', 'user'],
        routes: [
            { path: '/user', redirect: '/user/login' },
            // 可以多层嵌套
            { path: '/user/login', name: 'login', component: './User/Login', icon: '' },
        ]
    },
]
```

#### mock

调试工具

```js
const getNotice = [
  { id: 'xxx1' },
  { id: 'xxx2' },
  { id: 'xxx3' },
  { id: 'xxx4' },
  { id: 'xxx5' },
  { id: 'xxx6' },
];
// 通过访问对应的接口获得对应的数据
export default {
  'GET /api/project/notice': getNotice,
}
```

#### public

/public/favicon.png 

logo图案

## src

#### pages

- 连接至redux

```js
@connect(({ login, loading }) => ({
  login,
  submitting: loading.effects['login/login'],
}))
class LoginPage extends Component {
    // 可以使用this.props.login访问其中的内容
}
```

- 通过dispatch发送异步请求

```js
  handleSubmit = (err, values) => {
    const { type } = this.state;
    if (!err) {
      const { dispatch } = this.props;
      dispatch({
        type: 'login/login',
        payload: {
          ...values,
          type,
        },
      });
    }
  };
```

#### models

redux状态管理, 导入servers方法发送请求, 并将状态进行更新

```js
import {queryDemoUserList} from "@/services/demo";

export default {
    // 名称
    namespace: 'demo',
    // 状态
    state: {
        userList: [],
        page: 1,
        totalPage: 1,
    },
    // 异步请求
    effects: {
        *getUserList({ payload }, { call, put }) {
            const response = yield call(queryDemoUserList, payload);
      		console.log(response);
            yield put({
                type: 'queryUserList',
                payload: response,
            })
        },
    },
    // 对状态进行更新
    reducers: {
        queryUserList(state, { payload }) {
            return payload
        },
    },
}
```

#### servers

发送请求

```js
import { stringify } from 'qs';
import request from '@/utils/request';
import getHeaders from "@/services/readCook";
// get请求
export async function queryDemoUserList(params) {
    return request(`http://127.0.0.1:5000/users?${stringify(params)}`, {
        headers: getHeaders()
    });
}
// patch请求
export async function queryDemoModifyUser(params) {
    return request('http://127.0.0.1:5000/user', {
        method: "PATCH",
        body: JSON.stringify(params),
        mode: 'cors',
        credentials: 'include',
        headers: getHeaders()
    });
}
// delete请求
export async function queryDemoDeleteUser(params) {
  	return request(`http://127.0.0.1:5000/user?${stringify(params)}`, {
    	method: "DELETE",
   	 	mode: 'cors',
    	headers: getHeaders(),
  	});
}
// post请求
export async function fakeRegister(params) {
  	return request('http://127.0.0.1:5000/register', {
    	method: 'POST',
    	data: params,
    	headers: getHeaders()
  	});
}
```

#### defaultSettings

```js
// true为关闭国际化
menu: {
	disableLocal: true,
},
// 项目名称
title: 'MyProject',
```

