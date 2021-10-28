# 解析库的使用

## XPath使用

1. 全称XML Path Language, 就是XML路径语言

2. xpath常用规则

   1. `nodename`: 选取此节点的所有子节点
   2. `/`: 从当前节点选取直接子节点
   3. `//`: 从当前节点选取子孙节点
   4. `.`: 选取当前节点
   5. `..`: 选取当前节点的父节点
   6. `@`: 选取属性

3. 实例规则

   1. `//title[@lang='eng']`

      * 选择所有名称为title, 同时属性lang的值为eng的节点

        ```html
            <div>
                <ul>
                    <li class="item-0"><a href="link1.html"></a>first item</li>
                    <li class="item-1"><a href="link2.html"></a>second item</li>
                    <li class="item-inactive"><a href="link3.html"></a>third item</li>
                    <li class="item-1"><a href="link4.html"></a>fourth item</li>
                    <li class="item-0"><a href="link5.html"></a>fifth item</li>
                </ul>  
            </div>
        ```

        ```python
        from lxml import etree
        html = etree.HTML(text)
        result = etree.toString(html)	// 修正html, 结果是bytes类型
        ```

   2. 直接读取文本文件解析

      ```python
      from lxml import etree
      html = etree.parse('./test.html', etree.HTMLParser())
      result = etree.toString(html)
      ```

   3. 匹配所有节点

      ```python
      from lxml import etree
      html = etree.parse('./test.html', etree.HTMLParser())
      result = html.xpath('//*')
      print(result)
      ```

      ```python
      from lxml import etree
      html = etree.parse('./test.html', etree.HTMLParser())
      result = html.xpath('//li')
      print(result)
      ```

   4. 子节点

      ```python
      from lxml import etree
      html = etree.parse('./test.html', etree.HTMLParser())
      result = html.xpath('//li/a')
      ```

      

