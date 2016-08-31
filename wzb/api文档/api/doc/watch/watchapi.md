# 手表api服务

- 接口功能介绍
儿童手表rest api
- 服务协议
HTTP/GET
- URL
    http://lib.huayinghealth.com/lib-x/?service=watch.
- 编码格式
如无特殊声明,所有接口的输入参数和输出数据编码全部统一为utf-8

- 所有接口都带有sign参数,生成规则是所有参数按字典排序md5加密,32位小写字符串.
- service=xx.oo参数包含在内,sign参数不包含

## 1.获取最新的一次定位信息
## `?service=watch.get_lastest_location`
### 1.1 参数说明      

参数名称|说明|是否必须
---|---|----
imei|查询的手表imei,为15位数字|是
sign|参数签名|是
    
### 1.2 实例说明
- [http://lib.huayinghealth.com/lib-x/?service=watch.get_lastest_location&imei=358688000000158&sign=161f58141c659d9f97fbfd2d948efaa3](http://lib.huayinghealth.com/lib-x/?service=watch.get_lastest_location&imei=358688000000158&sign=161f58141c659d9f97fbfd2d948efaa3)
    

### 1.3 返回值说明
    {"ret":200,"data":{"code":0,"message":[{"watch_time":"2016-08-24 16:47:30","location_lon":"113.9749712","location_lat":"22.5617714","location_type":"1","location_content":"广东省 深圳市 南山区 龙珠四路 靠近金谷创业园","battery":"100"}],"info":""},"msg":""}
- ret   200:解析正常; 其他:异常或错误
- data  查询结果
- code  0:有查询结果;1:无查询结果
- message:查询内容
- watch_time 手表定位时间
- locaton_lon 经度
- location_lat 纬度
- location_type 定位类型: 0:gps定位;1:wifi定位;2:基站定位
- location_content 位置描述
- battery 电量百分比
        
## 2.获取某一天时间内的所有定位坐标
## `?service=watch.get_day_location`
### 2.1 参数说明
参数名称|说明|是否必须
---|---|---
imei|查询的手表Imei,为15位数字|是
date|查询的日期,为2016-08-24 格式|是
sign|接口签名|是
    
### 2.2 实例说明
- [http://lib.huayinghealth.com/lib-x/?service=watch.get_day_location&imei=358688000000158&date=2016-08-24](http://lib.huayinghealth.com/lib-x/?service=watch.get_day_location&imei=358688000000158&date=2016-08-24)
    
### 2.3 返回值说明
    {"ret":200,"data":{"code":0,"message":[{"location_lon":"113.9749034","location_lat":"22.5618319"},{"location_lon":"113.9747439","location_lat":"22.56185"},{"location_lon":"113.9748009","location_lat":"22.5614014"},{"location_lon":"113.9746219","location_lat":"22.5618438"},{"location_lon":"113.9747534","location_lat":"22.5614326"},{"location_lon":"113.974975","location_lat":"22.5617508"},{"location_lon":"113.9747461","location_lat":"22.5613574"},{"location_lon":"113.9749314","location_lat":"22.5616165"},{"location_lon":"113.9747876","location_lat":"22.561406"},{"location_lon":"113.9747662","location_lat":"22.5613498"},{"location_lon":"113.9747396","location_lat":"22.5618226"},{"location_lon":"113.9748164","location_lat":"22.5617638"},{"location_lon":"113.9749824","location_lat":"22.5617573"},{"location_lon":"113.9747575","location_lat":"22.5613523"},{"location_lon":"113.9747312","location_lat":"22.5613612"},{"location_lon":"113.9747629","location_lat":"22.561349"},{"location_lon":"113.9749712","location_lat":"22.5617714"}],"info":""},"msg":""}
- ret  200:解析正常;其他:异常或错误
- data 解析结果
- code 0:查询有结果;1:查询无结果;2:日期参数错误
- message 坐标数组
- location_lon 经度
- location_lat 纬度
        
## 3.获取手表在线状态
## `?service=watch.is_online`
### 3.1 参数说明
参数名称|说明|是否必须
--|--|--
imei|查询的手表imei,为15位数字|是
sign|接口签名|是
### 3.2实例说明
[http://lib.huayinghealth.com/lib-x/?service=watch.is_online&imei=358688000000158](http://lib.huayinghealth.com/lib-x/?service=watch.is_online&imei=358688000000158)
### 3.3 返回值说明
    {"ret":200,"data":{"code":0,"message":1,"info":""},"msg":""}
- ret  200:解析正常;其他:异常或错误
- data 解析结果
- code 0:查询有结果;1:查询无结果;
- message 1:在线;0:不在线
    
## 4.设置定位模式(1分钟,10分钟,1小时)
## `?service=watch.set_upload_mode`
### 4.1 参数说明
参数名称|说明|是否必须
--|--|--
imei|手表imei,为15位数字|是
upmode|定位模式,为1,10,60 三种数字|是
sign|接口签名|是
### 4.2 实例说明
[http://lib.huayinghealth.com/lib-x/?service=watch.set_upload_mode&imei=358688000000159&upmode=10](http://lib.huayinghealth.com/lib-x/?service=watch.set_upload_mode&imei=358688000000159&upmode=10)
- 设为10分钟定位一次模式
    
### 4.3 返回值说明
    {"ret":200,"data":{"code":0,"message":"","info":""},"msg":""}
- ret  200:解析正常;其他:异常或错误
- data 解析结果
- code 0:设置成功;1:设备离线状态;2:参数错误