```shell
# 01 shell
scrapy startproject wangyi
```

```python
# 02 items.py
import scrapy
class WangyiItem(scrapy.Item):
    name = scrapy.Field()
    link = scrapy.Field()
```

```shell
# 03 shell
scrapy genspider job 163.com
```

```python
# 04 job.py
import scrapy
from wangyi.items import WangyiItem
class JobSpider(scrapy.Spider):
    name = 'job'
    allowed_domains = '163.com'
    start_url = 'https://hr.163.com/position/list,do'
    def parse(self, response):
        node_list = response.xpath()
        for num, node in enumerate(node_list):
            if num  % 2 ==0:
                item = WangyiItem()
                item['name'] = node.xpath().extract_first()
                yield item
       part_url = response.xpath().extract_first()
    	if part_url != 'javascript:void(0)':
            next_url = response.urljob(part_url)
            yield scrapy.Request(
            	url = next_url
                callback = self.parse
            )
```

```python
05 pipliense.py
import json
class WangyiPipeline(object):
    def __init__(self):
        self.file = open(src, 'w')
    def process_item(self, item, spider):
        item = dic(item)
        str_data = json.dumps(item, ensure_ascii=False) + ',/n'
        self.file.write(str_data)
    def __del__(self):
        self.file.close()
```

```python
06 settings.py
ITEM_PIPELINES = {
    'wangyi.pipeline.WangyiPipeline' : 300
}
```

```shell
scrapy crawl job	
```

