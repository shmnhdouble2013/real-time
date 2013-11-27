## 综述

RealTime 是一个实时模拟服务器时间组件，通过它你可以方便的获取当前的服务器时间，计算精度<=1秒。

* 版本：1.0
* 作者：水木年华double ```<huangjia2015@gmail.com>```
* demo：[http://gallery.kissyui.com/real-time/1.0/demo/index.html](http://gallery.kissyui.com/real-time/1.0/demo/index.html)


## 内置提供 3套时间更新模式，智能转换和性能优化，间隔性同步纠正本地计算服务器时间：

1. 本地时间----- 服务器初始化时间serviceTime配置项 和 更新url接口 都没配置情况下，则自动按照 计算机 本地时间 计算；  
2. 时间差模拟时间----- 配置服务器时间serviceTime，未配置时间更新url接口，则依据初始化时间差 计算模拟出服务器当前时间； 
3. ajax异步间隔性同步时间---- 配置url更新接口，则会 间隔性(默认1小时)同步更新校正本地模拟服务器时间，异步默认以 jsonp方式，避免跨域烦劳；  
	   

## 初始化组件

```javascript
S.use('gallery/real-time/1.0/index', function (S, RealTime) {
    var real-time = new RealTime({
     		serviceTime: S.now(),  // 支持  时间字符串 或者 毫秒数 2种方式
            url: url    
     	});
});
```

## API说明 --- 配置参数

```javascript
// 默认配置
var defCfg = {

    // 服务器初始化时间 默认 毫秒数number、 支持 标准时间字符串如：'2013-11-20 17:30:32'
    serviceTime: null,

    // 服务器时间接口 --默认
    url: '',
	
	// 是否是jsonp  --默认
	isJsonp: true,
	
	// 是否开启 自动更新  --默认
	isAutoUpdate: true,
	
    // 异步更新服务器时间 配置，最低间隔 需要 >= 1分钟 -- 默认1小时
    ajaxUpMinutes: 60,

    // 本地时间更新频率 秒  --默认
    localTimeUpdate: 1              
};
```    


## API说明 --- 主要方法
    
```javascript

// 开启时间 自动更新
startAutoUpdateUi();

// 停止 自动更新
stopAutoUpdateUi();

// 获取服务器时间 -- 毫秒数 ps:当为本地时间模式时 返回null
getCurrTime();

// 获取当前时间 年月日 字符串  ps：若传递日期毫秒数参数时，则会 输出 传入毫秒数的转化的 年月日 日期字符串
getTimeYMDstr();

// 获取当前时间 时分秒 字符串 ps：若传递 时分秒 毫秒数参数时，则会 输出 传入毫秒数的转化的 时分秒 字符串
getCurrTimeHMSstr();

// 获取 服务器 与 本地差异 -- 毫秒数  ps:无差异时候 返回null
getServerLocalDiff();
```

## API说明 -- 事件

```javascript
/**  
* 本地时间更新 模式发生
* @event localTimeUpdateMod 
* @param {number} ev.time 当前时间
*/
'localTimeUpdateMod'

/**  
* 异步更新服务器时间 模式发生
* @event ajaxTimeUpdateMod  
* @param {number} ev.time 当前时间
*/
'ajaxTimeUpdateMod'
```

## API说明 --- 其他时间方法列举

```javascript
/**
* 根据日期毫秒数，获取 具体时间 字符串信息 
* @method getDateStr(number); 
* @param {number}日期毫秒数
* @return {string} 'yyyy-mm-dd h:m:s'
*/ 
getDateStr();

// 根据日期时间字符串 返回日期对象 毫秒数
getDateParse();

/**
* 根据时分秒 残缺信息 自动补全完整 合法时间字符串
* @method autoComplement(hour, minutes, seconds, isHideSeconds);
* @param {string} 时间字符串 小时 '3'
* @param {string} 时间字符串 分钟 '19'
* @param {string} 时间字符串 秒 null
* @param {boolean} 是否不显示秒 默认为true
* @return {string} 时分秒字符串 如： '03:19:00'
**/ 
autoComplement(hour, minutes, seconds, isHideSeconds);


/**
* 根据 时分秒 字符串 获取毫秒数
* @method getMillisecond(str)
* @param {str} 时分秒 时间
* @return {number} 时分秒 毫秒数 之和
*/
getMillisecond(str);


/**
* 根据 时分秒 毫秒数 获取 时分 字符串
* @method getHMstr(number)
* @param {number} 时分秒 毫秒数
* @return {string} 时分 字符串
*/
getHMstr(number);
```
