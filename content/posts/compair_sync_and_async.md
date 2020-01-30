+++
title = "比较同步编程和异步编程的区别"
date = "2015-12-23T15:21:01+08:00"
tags = ["coding"]
categories = ["geek"]
draft = false
+++

> Sync in C

```C
#include <time.h>
#include <stdio.h>
#include <unistd.h>
int main()
{
    int i;
    time_t the_time;
    for(i = 1; i <= 10; i++) {
        the_time = time((time_t *)0);
        printf("The time is %ld\n", the_time);
        sleep(2);
    }
    exit(0);
}
```

    The time is 1396492137
    The time is 1396492139
    The time is 1396492141
    The time is 1396492143
    The time is 1396492145
    The time is 1396492147
    The time is 1396492149
    The time is 1396492151
    The time is 1396492153
    The time is 1396492155

# Async in javascript

```javascript
function test() {
  for (var i = 0; i < 10; i++) {
    console.log(new Date());
    setTimeout(function() {}, 2000); //睡眠2秒，然后再进行一下次for循环打印
  }
}
test();
```

    Wed Dec 23 2015 15:27:15 GMT+0800 (CST)
    Wed Dec 23 2015 15:27:15 GMT+0800 (CST)
    Wed Dec 23 2015 15:27:15 GMT+0800 (CST)
    Wed Dec 23 2015 15:27:15 GMT+0800 (CST)
    Wed Dec 23 2015 15:27:15 GMT+0800 (CST)
    Wed Dec 23 2015 15:27:15 GMT+0800 (CST)
    Wed Dec 23 2015 15:27:15 GMT+0800 (CST)
    Wed Dec 23 2015 15:27:15 GMT+0800 (CST)
    Wed Dec 23 2015 15:27:15 GMT+0800 (CST)
    Wed Dec 23 2015 15:27:15 GMT+0800 (CST)
