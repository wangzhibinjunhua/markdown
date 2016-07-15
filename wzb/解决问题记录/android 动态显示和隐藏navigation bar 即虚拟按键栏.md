# android 动态显示和隐藏navigation bar 即虚拟按键栏

## 1.navigationbar 是在systemui里面显示的
 - 路径:\frameworks\base\packages\SystemUI\src\com\android\systemui\statusbar\phone\PhoneStatusBar.java
            
        
## 2.封装接口出来给第三方应用使用   
- 注册两个广播
>
```
//add by wzb for hide or show navigationbar
        filter.addAction("android.intent.action.custom_nvbar_hide");
        filter.addAction("android.intent.action.custom_nvbar_show");
```

                
- 在接收广播的地方进行处理
>  
```
else if("android.intent.action.custom_nvbar_hide".equals(action)){
                if (mNavigationBarView !=null && nvbar_flag){
                    mWindowManager.removeView(mNavigationBarView);
                    mNavigationBarView = null;
                    nvbar_flag=false;
                }
            }
            else if("android.intent.action.custom_nvbar_show".equals(action)){
                if(mNavigationBarView == null && !nvbar_flag){
                     mNavigationBarView =
                    (NavigationBarView) View.inflate(mContext, R.layout.navigation_bar, null);

                    mNavigationBarView.setDisabledFlags(mDisabled);
                    mNavigationBarView.setBar(PhoneStatusBar.this);
                    addNavigationBar();
                    nvbar_flag=true;
                }
            }
```


#### powered by wzb@lib-x.com 
