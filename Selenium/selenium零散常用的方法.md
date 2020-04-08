# selenium使用

## 零散常用的方法

from selenium import webdriver

### 调用键盘按键操作时需要引入的Keys包

from selenium.webdriver.common.keys import Keys

### 创建指定浏览器对象

driver = webdriver.Chrome()
driver = webdriver.Chrome(executable_path="./chromedriver"))

### 获取当前页面的url

driver.current_url

### 页面前进后退 

driver.forward()     #前进
driver.back()        # 后退

### 关闭页面

driver.close()  关闭当前页面
driver.quit()  退出整个浏览器

### 获取新的页面快照

driver.save_screenshot("xxx.png")

### 打印网页渲染后的源代码

print driver.page_source

### 获取页面名为 wrapper的id标签的文本内容

data = driver.find_element_by_id("wrapper").text

### 打印页面标题

print driver.title

### ctrl+a 全选输入框内容

driver.find_element_by_id("kw").send_keys(Keys.CONTROL,'a')

### ctrl+x 剪切输入框内容

driver.find_element_by_id("kw").send_keys(Keys.CONTROL,'x')

### 输入框重新输入内容

driver.find_element_by_id("kw").send_keys("xxx")

### 模拟Enter回车键

driver.find_element_by_id("su").send_keys(Keys.RETURN)
