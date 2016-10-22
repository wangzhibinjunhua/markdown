# 手表api服务

- 接口功能介绍
儿童手表rest api
- 服务协议
HTTP/GET
- URL
    http://lib.huayinghealth.com/lib-x/?service=watch.
- 编码格式
如无特殊声明,所有接口的输入参数和输出数据编码全部统一为utf-8

- 所有接口都带有sign参数,生成规则是所有参数名称按字典排序md5加密,32位小写字符串.
- service=xx.oo参数包含在内,sign参数不包含
- 举例: 参数service=xxx&upmode=10&imei=13123123 参数名称升序排序 imei <service< upmode.   拼接内容为字符串str=13123123xxx10. 然后计算str的md5,32位小写  

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
    
## 5.监听
## `?service=watch.monitor`
### 5.1 参数说明
参数名称|说明|是否必须
--|--|--
imei|手表imei,为15位数字|是
phonenumber|手表回拨的电话号码|是
sign|接口签名|是
    
### 5.2 实例说明
[http://lib.huayinghealth.com/lib-x/?service=watch.monitor&imei=358688000000159&phonenumber=13800001234](http://lib.huayinghealth.com/lib-x/?service=watch.monitor&imei=358688000000159&phonenumber=13800001234)
### 5.3 返回值说明
    {"ret":200,"data":{"code":0,"message":"","info":""},"msg":""}
- ret  200:解析正常;其他:异常或错误
- data 解析结果
- code 0:设置成功;1:设备离线状态;2:参数错误
        
## 6.设置sos号码
## `?service=watch.set_sos_number`
### 6.1 参数说明
参数名称|说明|是否必须
--|--|--
imei|手表Imei|是
sos|sos号码,最多三个,以,隔开.例子:123456,123456,123456|是
sign|接口签名|是
### 6.2 实例说明
[http://lib.huayinghealth.com/lib-x/?service=watch.set_sos_number&imei=358688000000159&sos=13800001234,123456,222365](http://lib.huayinghealth.com/lib-x/?service=watch.set_sos_number&imei=358688000000159&sos=13800001234,123456,222365)
### 6.3 返回值说明
    {"ret":200,"data":{"code":0,"message":"","info":""},"msg":""}
- ret  200:解析正常;其他:异常或错误
- data 解析结果
- code 0:设置成功;1:设备离线状态;2:参数错误
    
## 7.恢复出厂设置
## `?service=watch.reset`
### 7.1 参数说明
参数名称|说明|是否必须
--|--|--
imei|手表imei|是
sign|接口签名|是
    
### 7.2 实例说明
[http://lib.huayinghealth.com/lib-x/?service=watch.reset&imei=358688000000159](http://lib.huayinghealth.com/lib-x/?service=watch.reset&imei=358688000000159)
### 7.3 返回值说明
    {"ret":200,"data":{"code":0,"message":"","info":""},"msg":""}
- ret  200:解析正常;其他:异常或错误
- data 解析结果
- code 0:设置成功;1:设备离线状态;2:参数错误
    
## 8.重启手表
## `?service=watch.reboot`
### 8.1 参数说明
参数名称|说明|是否必须
--|--|--
imei|手表imei|是
sign|接口签名|是
    
### 8.2 实例说明
[http://lib.huayinghealth.com/lib-x/?service=watch.reboot&imei=358688000000159](http://lib.huayinghealth.com/lib-x/?service=watch.reboot&imei=358688000000159)
### 8.3 返回值说明
    {"ret":200,"data":{"code":0,"message":"","info":""},"msg":""}
- ret  200:解析正常;其他:异常或错误
- data 解析结果
- code 0:设置成功;1:设备离线状态;2:参数错误

## 9.请求定位
## `?service=watch.req_location`
### 9.1 参数说明
参数名称|说明|是否必须
--|--|--
imei|手表imei|是
sign|接口签名|是
    
### 9.2 实例说明
[http://lib.huayinghealth.com/lib-x/?service=watch.req_location&imei=358688000000159](http://lib.huayinghealth.com/lib-x/?service=watch.req_location&imei=358688000000159)
### 9.3 返回值说明
    {"ret":200,"data":{"code":0,"message":"","info":""},"msg":""}
- ret  200:解析正常;其他:异常或错误
- data 解析结果
- code 0:设置成功;1:设备离线状态;2:参数错误

## 10.关机
## `?service=watch.shutdown`
### 10.1 参数说明
参数名称|说明|是否必须
--|--|--
imei|手表imei|是
sign|接口签名|是
    
### 10.2 实例说明
[http://lib.huayinghealth.com/lib-x/?service=watch.shutdown&imei=358688000000159](http://lib.huayinghealth.com/lib-x/?service=watch.shutdown&imei=358688000000159)
### 10.3 返回值说明
    {"ret":200,"data":{"code":0,"message":"","info":""},"msg":""}
- ret  200:解析正常;其他:异常或错误
- data 解析结果
- code 0:设置成功;1:设备离线状态;2:参数错误
    
## 11.找手表
## `?service=watch.find_dev`
### 11.1 参数说明
参数名称|说明|是否必须
--|--|--
imei|手表imei|是
sign|接口签名|是
    
### 11.2 实例说明
[http://lib.huayinghealth.com/lib-x/?service=watch.find_dev&imei=358688000000159](http://lib.huayinghealth.com/lib-x/?service=watch.find_dev&imei=358688000000159)
### 11.3 返回值说明
    {"ret":200,"data":{"code":0,"message":"","info":""},"msg":""}
- ret  200:解析正常;其他:异常或错误
- data 解析结果
- code 0:设置成功;1:设备离线状态;2:参数错误
    
## 12.设置闹钟
## `?service=watch.set_alarm`
### 12.1 参数说明
参数名称|说明|是否必须
--|--|--
imei|手表imei|是
alarm|设置的闹钟,格式为08:10-1-1,08:10-1-2,08:10-1-3-0111110 多组闹钟之间用逗号隔开.`解释:08:10:闹钟时间为8点10分`;第二个1代表开启,0代表关闭.第三个数字1,2,3 代表三种类型,1:只闹一次;2:每天闹;3:自定义时间,后面0111110代表周一-周五闹,周日和周六不闹|是
sign|接口签名|是
    
### 12.2 实例说明
[http://lib.huayinghealth.com/lib-x/?service=watch.set_alarm&imei=358688000000159&alarm=08:00-1-1](http://lib.huayinghealth.com/lib-x/?service=watch.set_alarm&imei=358688000000159&alarm=08:00-1-1)
### 12.3 返回值说明
    {"ret":200,"data":{"code":0,"message":"","info":""},"msg":""}
- ret  200:解析正常;其他:异常或错误
- data 解析结果
- code 0:设置成功;1:设备离线状态;2:参数错误
    
## 13.设置电话本(前五个)
## `?service=watch.set_contact_a`
### 13.1 参数说明
参数名称|说明|是否必须
--|--|--
imei|手表imei|是
contacta|联系人,格式为 姓名1,电话1,姓名2,电话2,姓名3,电话3,姓名4,电话4,姓名5,电话5.姓名为fffe格式的unicode码,电话为数字|是
sign|接口签名|是
    
### 13.2 实例说明
[http://lib.huayinghealth.com/lib-x/?service=watch.set_contact_a&imei=358688000000159&contacta=8b730f5c,123,8b730f5c,125](http://lib.huayinghealth.com/lib-x/?service=watch.set_contact_a&imei=358688000000159&contacta=8b730f5c,123,8b730f5c,125)
- 8b730f5c 为中文 王小 unicode码 fffe格式的 每个字符占四位unicode

### 13.3 返回值说明
    {"ret":200,"data":{"code":0,"message":"","info":""},"msg":""}
- ret  200:解析正常;其他:异常或错误
- data 解析结果
- code 0:设置成功;1:设备离线状态;2:参数错误
    
## 14.设置电话本(后五个)
## `?service=watch.set_contact_b`
### 14.1 参数说明
参数名称|说明|是否必须
--|--|--
imei|手表imei|是
contactb|联系人,格式为 姓名1,电话1,姓名2,电话2,姓名3,电话3,姓名4,电话4,姓名5,电话5.姓名为fffe格式的unicode码,电话为数字|是
sign|接口签名|是
    
### 14.2 实例说明
[http://lib.huayinghealth.com/lib-x/?service=watch.set_contact_b&imei=358688000000159&contactb=8b730f5c,123,8b730f5c,125](http://lib.huayinghealth.com/lib-x/?service=watch.set_contact_b&imei=358688000000159&contactb=8b730f5c,123,8b730f5c,125)
- 8b730f5c 为中文 王小 unicode码 fffe格式的 每个字符占四位unicode

### 14.3 返回值说明
    {"ret":200,"data":{"code":0,"message":"","info":""},"msg":""}
- ret  200:解析正常;其他:异常或错误
- data 解析结果
- code 0:设置成功;1:设备离线状态;2:参数错误
    
## 15.发送文本消息
## `?service=watch.send_msg`
### 15.1 参数说明
参数名称|说明|是否必须
--|--|--
imei|手表imei|是
message|发送的消息,unicode码,每个字符占4位,例如:你好(604f7d59)|是
sign|接口签名|是
    
### 15.2 实例说明
[http://lib.huayinghealth.com/lib-x/?service=watch.send_msg&imei=358688000000159&message=604f7d59](http://lib.huayinghealth.com/lib-x/?service=watch.send_msg&imei=358688000000159&message=604f7d59)
### 15.3 返回值说明
    {"ret":200,"data":{"code":0,"message":"","info":""},"msg":""}
- ret  200:解析正常;其他:异常或错误
- data 解析结果
- code 0:设置成功;1:设备离线状态;2:参数错误
    
## 16.增加小红花
## `?service=watch.add_honor`
### 16.1 参数说明
参数名称|说明|是否必须
--|--|--
imei|手表imei|是
sign|接口签名|是
    
### 16.2 实例说明
[http://lib.huayinghealth.com/lib-x/?service=watch.add_honor&imei=358688000000159](http://lib.huayinghealth.com/lib-x/?service=watch.add_honor&imei=358688000000159)
- 增加一朵小红花
    
### 16.3 返回值说明
    {"ret":200,"data":{"code":0,"message":"","info":""},"msg":""}
- ret  200:解析正常;其他:异常或错误
- data 解析结果
- code 0:设置成功;1:设备离线状态;2:参数错误
    
## 17.清零小红花
## `?service=watch.clear_honor`
### 17.1 参数说明
参数名称|说明|是否必须
--|--|--
imei|手表imei|是
sign|接口签名|是
    
### 17.2 实例说明
[http://lib.huayinghealth.com/lib-x/?service=watch.clear_honor&imei=358688000000159](http://lib.huayinghealth.com/lib-x/?service=watch.clear_honor&imei=358688000000159)
- 清零小红花
    
### 17.3 返回值说明
    {"ret":200,"data":{"code":0,"message":"","info":""},"msg":""}
- ret  200:解析正常;其他:异常或错误
- data 解析结果
- code 0:设置成功;1:设备离线状态;2:参数错误
    
## 18.设置免打扰时间
## `?service=watch.set_silence`
### 18.1 参数说明
参数名称|说明|是否必须
--|--|--
imei|手表imei|是
silence|设置的免打扰时间段,多组之间用逗号隔开.例如:`21:10-07:30,09:00-12:00,14:00-16:00`|是
sign|接口签名|是
    
### 18.2 实例说明
    http://lib.huayinghealth.com/lib-x/?service=watch.set_silence&imei=358688000000159&silence=21:10-07:30,09:00-12:00,14:00-16:00

    
### 18.3 返回值说明
    {"ret":200,"data":{"code":0,"message":"","info":""},"msg":""}
- ret  200:解析正常;其他:异常或错误
- data 解析结果
- code 0:设置成功;1:设备离线状态;2:参数错误
    
## 19.获取新微聊信息列表
## `?service=watch.get_new_message_list`
### 19.1 参数说明
参数名称|说明|是否必须
--|--|--
imei|手表imei|是
user_id|app帐号(注册的手机号)|是
sign|接口签名|是
    
### 19.2 实例说明
   `http://lib.huayinghealth.com/lib-x/?service=watch.get_new_message_list&imei=123456789012345&user_id=13112345678`

    
### 19.3 返回值说明
    {"ret":200,"data":{"code":0,"message":[{"file":"123456789012345_1474532952.amr"},{"file":"123456789012345_1474532953.amr"},{"file":"123456789012345_1474532954.amr"}],"info":""},"msg":""}
- ret  200:解析正常;其他:异常或错误
- data 解析结果
- code 0:有新消息;1:无新消息;2:参数错误
- message:新消息文件名称filename
    
###特别说明
- 语音文件位置:`http://core.huayinghealth.com/media/childwatch/filename`
- 可直接下载,amr格式音频文件,新增jpg格式图片文件
- 关于离线消息,手表可发离线消息保存在服务器,app在连上网络时自行调用这个接口查询是否有新消息,有新消息就down下来
- down一个文件filename后,需要调用接口
- `http://lib.huayinghealth.com/lib-x/?service=watch.ignore_message&imei=123456789012345&user_id=13112345678&filename=123456789012345_1474527618.amr`
- 参数同上,多一个filename参数即为down下来的音频文件名称.
- 返回值{"ret":200,"data":{"code":0,"message":"","info":""},"msg":""}
- ret 200:解析正常
- code 0:处理正常
    

## 20.绑定手表
## `?service=watch.bind_watch`
### 20.1 参数说明
参数名称|说明|是否必须
--|--|--
imei|手表imei|是
user_id|app帐号(注册的手机号)|是
sign|接口签名|是
    
### 20.2 实例说明
    http://lib.huayinghealth.com/lib-x/?service=watch.bind_watch&imei=987654321012345&user_id=121212121

    
### 20.3 返回值说明
    {"ret":200,"data":{"code":0,"message":"","info":""},"msg":""}
- ret  200:解析正常;其他:异常或错误
- data 解析结果
- code 0:绑定成功;1:绑定错误或者已绑定;2:参数错误

## 21.解绑手表
## `?service=watch.unbind_watch`
### 21.1 参数说明
参数名称|说明|是否必须
--|--|--
imei|手表imei|是
user_id|app帐号(注册的手机号)|是
sign|接口签名|是
    
### 21.2 实例说明
    http://lib.huayinghealth.com/lib-x/?service=watch.unbind_watch&imei=987654321012345&user_id=121212121

    
### 21.3 返回值说明
    {"ret":200,"data":{"code":0,"message":"","info":""},"msg":""}
- ret  200:解析正常;其他:异常或错误
- data 解析结果
- code 0:解绑成功;1:错误或者本身没有绑定;2:参数错误   
    
## 22.远程拍照
## `?service=watch.remote_photo`
### 22.1 参数说明
参数名称|说明|是否必须
--|--|--
imei|手表imei|是
sign|接口签名|是
    
### 22.2 实例说明
[http://lib.huayinghealth.com/lib-x/?service=watch.remote_photo&imei=123456789012345](http://lib.huayinghealth.com/lib-x/?service=watch.remote_photo&imei=123456789012345)
- 控制手表拍照并发送到服务器
    
### 22.3 返回值说明
    {"ret":200,"data":{"code":0,"message":"","info":""},"msg":""}
- ret  200:解析正常;其他:异常或错误
- data 解析结果
- code 0:设置成功;1:设备离线状态;2:参数错误

  

    
    
