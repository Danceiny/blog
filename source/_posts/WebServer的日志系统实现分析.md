---
date: 2017-07-04 20:03:26
status: public
title: WebServer的日志系统实现分析
keywords: 
- 后台
- Web
- 日志
- log
tags: 

categories: 
---

```python
@Singleton
class LogCenter(object):
    def __init__(self):
        self.logger_map = {}

    def get_logger(self, name):
        """ return logger"""
        if not self.logger_map.has_key(name):
            self.logger_map[name] = MyLogger(name)
        return self.logger_map[name]
# Usage:
# data_logger = LogCenter.instance().get_logger('DataControlerLog')
# except Exception,e:
#   data_logger.error("Data Controler delete data error, msg=[%s]" % ,repr(e)))
#   result['code'] = ED.err_sys
```