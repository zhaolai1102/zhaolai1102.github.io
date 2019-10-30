---
layout:     post                  #不要管他
title:      redux     #标题
subtitle:   react-redux              #别名,简介,标题下面的那一行字
date:       2019-10-24            #发表时间
author:     Zhaolai                    #作者
header-img: img/post-bg-rwd.jpg   #背景图片
catalog: true                     #导航目录,不要管他
original: true                    #是否原创申明
tags:                             #标签,可以有多个
    - react
    - react-redux
---

## 建立Provider

```js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';
import {Provider} from 'react-redux';
import store from "./component/store/store";

ReactDOM.render(<Provider store={store}><App /></Provider>, document.getElementById('root'));
serviceWorker.unregister();
```

## 建立store

```js
import { createStore } from 'redux';
import reducer from './reducer';

const store = createStore(reducer);
export default store;
```

## 建立reducer

```js
import md5 from 'js-md5';
// 默认值
const defaultState = {
    signature: md5('default'),
    platform: 1,
    guid: md5('default'),
    version: '1.0',
};
// 主要的方法
const reducer =  (state = defaultState , action) =>{
    if(action.type === "change_signature"){
        const newState = JSON.parse(JSON.stringify(state));
        newState.signature = action.signature;
        return newState;
    }
    if(action.type === "change_platform"){
        const newState = JSON.parse(JSON.stringify(state));
        newState.platform = action.platform;
        return newState;
    }
    if(action.type === "change_guid"){
        const newState = JSON.parse(JSON.stringify(state));
        newState.guid = action.guid;
        return newState;
    }
    if(action.type === "change_version"){
        const newState = JSON.parse(JSON.stringify(state));
        newState.version = action.version;
        return newState;
    }
    return state;
};
export default reducer
```

## 使用redux

```js
import React from 'react'
import errorList from "../../static/ErrorList";
import GetForm from "../../static/getForm";
import './Login.css';
import {connect} from "react-redux";

class Login extends React.Component {
    // eslint-disable-next-line no-useless-constructor
    constructor (props) {
        super(props);
        this.state = {
            username: '',
            password: '',
        }
    }
    onChangeUsername = (event) => {
        this.setState({
            username: event.target.value
        })
    };
    onChangePassword = (event) => {
        this.setState({
            password: event.target.value
        })
    };
    onClick = () => {
        // 获取redux的值
        let {signature, platform, version, guid} = this.props;
        let {username, password} = this.state;
        let getForm = new GetForm();
        let formData = getForm.getForm(username, password, signature, platform, version, guid);
        if (formData != null) {
            fetch("http://127.0.0.1:5000/login",{method:"POST", mode: "cors", body: formData})
                .then(response => response.json())
                .then(result => this.setSearchTopStories(result, username))
                .catch(e => e);
        }
    };

    setSearchTopStories = (result, username) => {
        let {change_signature, change_guid} = this.props;
        if (result['ServerNo'] === "SN200"){
            // 更换redux的值
            change_signature(result["ResultData"]["signature"]);
            change_guid(result["ResultData"]["guid"]);
            alert(result['ResultData']['info']);
        } else {
            alert(errorList[result['ServerNo']])
        }
    };
    render() {
        return (
            <div>
                <div className="header">
                    <div className="box">
                        <h1>Welcome To Login Page !</h1>
                    </div>
                </div>
                <form className="clear login" method="post">
                    <p>username:</p>
                    <label>
                        <input type="text" name="username" onChange={this.onChangeUsername}/>
                    </label>
                    <p>password:</p>
                    <label>
                        <input name="password" type="password" onChange={this.onChangePassword}/>
                    </label>
                    <button className="reset" type="reset">reset</button>
                    <span className="submit" onClick={this.onClick}>submit</span>
                </form>
            </div>
        )
    }
}

function mapStateToProps(state) {
    return state
}
//需要触发什么行为
function mapDispatchToProps(dispatch) {
    return {
        // 方法名: 参数 => dispatch({type: 类型, 键值对})
        change_signature: (signature) => dispatch({ type: 'change_signature', 'signature': signature }),
        change_guid: (guid) => dispatch({ type: 'change_guid', 'guid': guid }),
    }
}
export default Login = connect(mapStateToProps, mapDispatchToProps)(Login)
```

