# 逆地理编码
    
## 1.定位服务
- 接口功能介绍
根据上传经纬度坐标信息,定位服务返回位置信息
- 服务协议
HTTP/GET
- URL
    http://lib.huayinghealth.com/lib-x/?service=geocode.regeo
- 编码格式
如无特殊声明,所有接口的输入参数和输出数据编码全部统一为utf-8

        
## 2.接口参数说明
参数名|含义|规则说明|是否必须
----|----|----|----
location|经纬度坐标|规则： 最多支持20个坐标点。多个点之间用竖线分割。经度在前，纬度在后，经纬度间以,分割，经纬度小数点后不得超过6位|必填

    
## 3.实例说明
- [http://lib.huayinghealth.com/lib-x/?service=geocode.regeo&location=113.976019,22.559275](http://lib.huayinghealth.com/lib-x/?service=geocode.regeo&location=113.976019,22.559275)
- 返回 `{"ret":200,"data":{"status":"1","info":"OK","infocode":"10000","regeocode":{"formatted_address":"广东省深圳市南山区桃源街道龙井村","addressComponent":{"country":"中国","province":"广东省","city":"深圳市","citycode":"0755","district":"南山区","adcode":"440305","township":"桃源街道","towncode":"440305008000","neighborhood":{"name":"龙井村","type":"商务住宅;住宅区;住宅小区"},"building":{"name":[],"type":[]},"streetNumber":{"street":"龙珠五路","number":"36号","location":"113.975907,22.5593664","direction":"西北","distance":"15.3436"},"businessAreas":[{"location":"113.98060652702694,22.55827501351351","name":"桃源村","id":"440305"}]}}},"msg":""}`
    
## 4.返回值说明
- 无查询结果返回null
- 正常返回
![](http://api.huayinghealth.com/doc/map/geocode1.png)
![](http://api.huayinghealth.com/doc/map/geocode2.png)
![](http://api.huayinghealth.com/doc/map/geocode3.png)
![](http://api.huayinghealth.com/doc/map/geocode4.png)
![](http://api.huayinghealth.com/doc/map/geocode5.png)









