# 基站&wifi定位

## 1.定位服务
- 接口功能介绍
根据上传终端设备的基站/wifi等信息,定位服务返回位置信息
- 服务协议
HTTP/GET
- URL
    http://lib.huayinghealth.com/lib-x/?service=lbs.data
- 编码格式
如无特殊声明,所有接口的输入参数和输出数据编码全部统一为utf-8
## 2.接口参数说明
- 表一    
 
参数名称|含义|规则说明|是否必须|默认值
---|---|------|-------|----
bts|接入基站信息|见表二说明|必须|无
nearbts|附近基站信息|基站信息1\ 基站信息2|非必须|无
macs|wifi列表中wifi信息|只有填写2个及以上方可wifi定位|非必须|无
        
- 表二
        
参数|内部参数|说明
--|--|--
bts|bts=mcc,mnc,lac,cellid,signal|.
mcc|.|移动用户所属国家代码,中国460|
mnc|.|移动网号,中国移动:0,联通:1
lac|.|位置区域码,取值范围0-65535
cellid|.|基站小区编号,取值范围:0-65535,0-268435455,其中0,65535,268435455不使用,小区编码大于65535为3G基站
signal|.|信号强度,取值范围0到-113dbm
.|.|.
macs|macs=macaddress,signal,ssid|`f0:7d:68:9e:7d:18,-41,TPLink`
    
- 特别说明
macs 的wifi信息,多个wifi信息之间用|隔开
如`macs=58:6a:b1:a7:d8:90,-81,Richpad-work-2|8c:be:be:48:8b:0f,-71,juno_wifi1`

nearbts 多个基站信息之间也用|隔开,同上


## 3.实例说明
    http://lib.huayinghealth.com/lib-x/?service=lbs.data&bts=460,0,10145,3682,5&macs=58:6a:b1:a7:d8:90,-81,Richpad-work-2|8c:be:be:48:8b:0f,-71,juno_wifi1

- 返回值:`{"ret":200,"data":{"status":"1","info":"OK","infocode":"10000","result":{"type":"3","location":"113.975061,22.5615967","radius":"35","desc":"广东省 深圳市 南山区 龙珠五路 靠近金谷创业园","country":"中国","province":"广东省","city":"深圳市","citycode":"0755","adcode":"440305","road":"龙珠五路","street":"龙珠四路","poi":"金谷创业园"}},"msg":""}`
        
## 4.返回值说明
ret : 200 请求正确
data: 返回内容 json格式
data 内容分析
info -- 状态.ok表示正常
status --返回状态,值为1或0,0代表错误

result --定位结果
type 定位类型:3 wifi;4 基站
location 经纬度
radius 定位精度半径
desc 位置描述
