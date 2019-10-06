＃家国梦

##按键精灵脚本

## 家国梦自动刷橙脚本 自用勿喷
* 目前增加断网重连效率高许多，前天试了下大概7个多小时就刷完了
* 模拟器使用雷电模拟器，分辨率为720p
* 使用了紫梦插件的超级滑动（官方的滑动不太精准）
* 使用山海插件进行断网，用模拟器的话断网我感觉比较快，手机断网容易出现重新登陆
* 如果建筑坐标偏了 请适当增加`Touch`的延迟
* 本来想做火车判断，但是这样三种橙色货物拉完了只能等待50秒！也懒得想了！
## 代码
```
Import "shanhai.lua"
Import "zm.luae" 			//导入插件,只需执行一次
zm.Init 					//初始化插件,只需执行一次
	Dim count = 0,num = 0	//橙色货物  3CC1FF 紫色 FF989A 对应建筑7FFFFF  EAC254
While True
	/*Dim 火车,flag
	flag = FindColor(372, 982, 695, 1139, "3CC1FF|FF989A|EAC254", 0, 1, intX, intY)
	火车 = FindColor(372, 982, 695, 1139, "13C6DF", 0, 1, intX, intY)
	If 火车 > -1 And flag > -1 Then */
		Dim intX, intY,返回值	//橙色货物坐标		
		Dim intX1, intY1,返回值1	//货物对应建筑的坐标
		返回值=FindColor(340,928,682,1135, "3CC1FF",0, 1, intX, intY) //取橙色货物
		If 返回值 > -1 Then 
    		TracePrint "橙货-->坐标在"&intX&","&intY 
    		intX = intX + 51	//橙色货物对应的X坐标 
    		intY = intY + 85	//橙色货物对应的Y坐标
    		Touch intX, intY, 800	//按住货物来获取对应建筑坐标
			返回值1 = FindColor (95,322,634,783, "61FFA4", 0, 0.99, intX1, intY1) //根据对应的建筑绿色特效获取对应建筑的坐标
			If 返回值1 > -1 Then 
				TracePrint "建筑-->坐标在"&intX1&","&intY1
				num = num + 1
				For i = 1 To 3
    				zm.Swipe intX, intY, intX1, intY1,100
				Next
			End If
		Else
    		TracePrint "无货"
    		count = count + 1
		End If
 	
		If count > 2 Then 
			count = 0
	 		Call shanhai.ControlWifi(False)
			Call shanhai.ControlWifi(True)
			Delay 35000
		Else 
			Delay 500
		End If
		TracePrint "已搬运货物共"&num&"次"
	//End If	
Wend
```
