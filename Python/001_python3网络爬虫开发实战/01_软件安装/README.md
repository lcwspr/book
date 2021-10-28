# 开发环境配置

## 请求库安装

1. requests安装

2. selenium安装

   1. 安装python包

   2. 安装chromedriver

   3. 测试

      ```python
      from selenium import webdriver
      browser = webdriver.Chrome()
      ```

3. aiohttp: 异步web服务的库， async/awit关键字

   * 推荐
     * cchardet
     * diodns

## 解析库安装

1. lxml: 支持html和xml解析，支持XPath解析方式
   * `pip3 install lxml`
2. Beautiful Soup安装
3. pyquery安装

## tesserocr的安装

1. tesserocr是python的一个ocr识别库， 其实是对于tesseract做的一层pythonApi封装