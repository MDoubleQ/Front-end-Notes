## lesson01-func-to-obj

### 01-validate

```js
/**
 * Created by hjb2722404 on 2016/2/29.
 */
/*
*
* 函数式的编程
*
* 缺点：全局变量空间污染
*
* */
function checkForm(){
    checkName();
    checkEmail();
    checkPwd();
}

function checkName(){
    var name = document.getElementById("name").value;
    if(!name){
        alert("请输入正确的用户名");
        return false;
    }
}

function checkEmail(){
    var email = document.getElementById("email").value;
    if(!email){
        alert("请输入正确的邮箱");
        return false;
    }
}

function checkPwd(){
    var pwd = document.getElementById("pwd").value;
    if(!pwd){
        alert("请输入正确的密码");
        return false;
    }
}
```



### 02-validate_obj

```js
/**
 * Created by hjb2722404 on 2016/2/29.
 */

/*
*
* 用对象字面量给对象添加方法
*
* 调用方式：对象.方法
*
* 缺点：对象无法复用继承
* */

var CheckObject ={

    checkName:function(){
        var name = document.getElementById("name").value;
        if(!name){
            alert("请输入正确的用户名");
            return false;
        }
    },
    checkEmail:function(){
        var email = document.getElementById("email").value;
        if(!email){
            alert("请输入正确的邮箱");
            return false;
        }
    },
    checkPwd:function(){
        var pwd = document.getElementById("pwd").value;
        if(!pwd){
            alert("请输入正确的密码");
            return false;
        }
    }
};

function checkForm(){
    CheckObject.checkName();
    CheckObject.checkEmail();
    CheckObject.checkPwd();
}

//function checkName(){
//    var name = document.getElementById("name").value;
//    if(!name){
//        alert("请输入正确的密码");
//        return false;
//    }
//}
//
//function checkEmail(){
//    var email = document.getElementById("email").value;
//    if(!email){
//        alert("请输入正确的邮箱");
//        return false;
//    }
//}
//
//function checkPwd(){
//    var pwd = document.getElementById("pwd").value;
//    if(!pwd){
//        alert("请输入正确的邮箱");
//        return false;
//    }
//}
```

### 03-validate_obj_anothor

```js
```



### 04-validate_obj_anothor_up

### 05-validate_class_anothor

### 06-validate_class_anothor_proto

### 07-validate_class_anothor_proto_obj

### 08-validate_class_anothor_proto_obj_link