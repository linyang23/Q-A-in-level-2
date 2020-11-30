### 0011_mongodb千万级数据查询等待问题

- 从师兄哪里拿到一个数据库有上千万条数据，由于其存储格式有些不正规，于是发现正则查询一个里面不存在的数据需要大量时间
- 于是通过阅读源代码注释发现可以通过设置超时指标和抛出异常的方式跳过这些不存在的数据，以节省时间效率

```
# 查询relay是否在traceroute中

# 导入模块
import pymongo
# 连接数据库
client = pymongo.MongoClient("mongodb://127.0.0.1:27017/")
db = client["traceroute"]  # 注意这里是中括号不是圆括号
# 读取数据
col = db["traceroute"]
i = 0
with open(r'.\1113_jp.txt', 'r', encoding='utf-8') as lines:     
    for line in lines:
        c = line.split('.')
        d = c[0] + '.' + c[1] + '.' + c[2]  #此处我是想查询/24子网          
        try:
            res = col.find_one({"traceroute": {"$regex": '^' + d + ".*?"}}, max_time_ms=30000)  #设定30s的单次查询上限时间
        except pymongo.errors.ExecutionTimeout as identifier:
            i += 1
            print('超时')
            with open(r'.\trace_node.txt', 'a', encoding='utf-8') as outlines:
                outlines.write('第' + str(i) + "个ip——" + line.strip() + ': 数据库查找超时' + '\n')
        else:            
            i += 1
            print(i)
            print(line)
            with open(r'.\trace_node.txt', 'a', encoding='utf-8') as outlines:
                outlines.write('第' + str(i) + "个ip——" + line.strip() + ': 已找到 ' + str(res['traceroute']) + '\n')
```
效果如下：[!tracenode]()