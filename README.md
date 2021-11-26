# 充电桩数据爬取

## 主要功能
爬取闪开来电公众号中附近电站页面的充电桩信息，并进一步对数据进行格式化处理，最后封装成web，以json格式返回页面信息

## 闪开来电公众号附近电站界面

<img src="https://img2020.cnblogs.com/blog/2533408/202111/2533408-20211126174820174-1112136287.jpg" width="400" height="700" alt="微信小程序"/><br/>
<img src="https://img2020.cnblogs.com/blog/2533408/202111/2533408-20211126174311750-1410831514.jpg" width="400" height="700" alt="微信小程序"/><br/>
## 步骤
**1.通过requests请求爬取网页数据**

函数getHTMLText(self,url)：输入参数为闪开来电公众号中附近电站页面的url，返回页面信息，即充电桩信息
![](https://img2020.cnblogs.com/blog/2533408/202111/2533408-20211126171405325-562504231.png)

**2.爬取所有充电桩的id和name,以列表形式返回**

函数getStationlist(self)：使用re库以及正则表达式匹配得到所有充电桩的id和name，以列表形式返回，用于爬取每个充电桩数据（插口状态）

**3.爬取每个充电桩数据（插口状态）**

函数getstationState(self,stationId)：输入参数为充电桩的id，以该id参数与附近电站页面的url拼接得到该充电桩页面的url，访问该页面，得到该充电桩数据（插口状态），再进一步对数据进行提取，返回#返回得到空闲插口、占用插口、空闲插口占比列表
![](https://img2020.cnblogs.com/blog/2533408/202111/2533408-20211126172741543-921109884.png)

**4.生成最终结果**

函数retuslt(self,result)：输入参数为键为stationlist、值为空的字典，返回包含每个充电桩所有插口的状态信息（包括空闲插口、占用插口、空闲插口占比）的字典，便于最终形成json格式

**5.封装成web，建立服务器**

使用flask创建一个服务，赋值给APP，返回json格式页面信息

## 返回结果

![](https://img2020.cnblogs.com/blog/2533408/202111/2533408-20211126174529620-1714257359.png)

