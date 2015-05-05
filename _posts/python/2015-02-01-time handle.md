---
layout: post
title: Python time handle
category: python
tags: Python time
keywords: Python time 时间戳
description: mark
---

>Python时间，日期，时间戳之间转换 (常用收藏一下)


### 1.将字符串的时间转换为时间戳
    方法:
        a = "2013-10-10 23:40:00"
        将其转换为时间数组
        import time
        timeArray = time.strptime(a, "%Y-%m-%d %H:%M:%S")
    转换为时间戳:
    timeStamp = int(time.mktime(timeArray))
    timeStamp == 1381419600

### 2.字符串格式更改
    如a = "2013-10-10 23:40:00",想改为 a = "2013/10/10 23:40:00"
    方法:先转换为时间数组,然后转换为其他格式
    timeArray = time.strptime(a, "%Y-%m-%d %H:%M:%S")
    otherStyleTime = time.strftime("%Y/%m/%d %H:%M:%S", timeArray)
 
 
### 3.时间戳转换为指定格式日期:
    方法一:
        利用localtime()转换为时间数组,然后格式化为需要的格式,如
        timeStamp = 1381419600
        timeArray = time.localtime(timeStamp)
        otherStyleTime = time.strftime("%Y-%m-%d %H:%M:%S", timeArray)
        otherStyletime == "2013-10-10 23:40:00"
 
    方法二:
        import datetime
        timeStamp = 1381419600
        dateArray = datetime.datetime.utcfromtimestamp(timeStamp)
        otherStyleTime = dateArray.strftime("%Y-%m-%d %H:%M:%S")
        otherStyletime == "2013-10-10 23:40:00"
 
### 4.获取当前时间并转换为指定日期格式
    方法一:
        import time
        获得当前时间时间戳
        now = int(time.time())  ->这是时间戳
        转换为其他日期格式,如:"%Y-%m-%d %H:%M:%S"
        timeArray = time.localtime(timeStamp)
        otherStyleTime = time.strftime("%Y-%m-%d %H:%M:%S", timeArray)
 
    方法二:
        import datetime
        获得当前时间
        now = datetime.datetime.now()  ->这是时间数组格式
        转换为指定的格式:
        otherStyleTime = now.strftime("%Y-%m-%d %H:%M:%S")
 
### 5.获得三天前的时间
    方法:
        import time
        import datetime
        先获得时间数组格式的日期
        threeDayAgo = (datetime.datetime.now() - datetime.timedelta(days = 3))
        转换为时间戳:
            timeStamp = int(time.mktime(threeDayAgo.timetuple()))
        转换为其他字符串格式:
            otherStyleTime = threeDayAgo.strftime("%Y-%m-%d %H:%M:%S")
    注:timedelta()的参数有:days,hours,seconds,microseconds
 
### 6.给定时间戳,计算该时间的几天前时间:
    timeStamp = 1381419600
    先转换为datetime
    import datetime
    import time
    dateArray = datetime.datetime.utcfromtimestamp(timeStamp)
    threeDayAgo = dateArray - datetime.timedelta(days = 3)
    参考5,可以转换为其他的任意格式了