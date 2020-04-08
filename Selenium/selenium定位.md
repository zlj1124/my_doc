# selenium使用

## 元素定位

from selenium.webdriver.common.by import By

### 1.通过id来查找

driver.find_element_by_id('kw')
driver.find_element(By.ID,'kw')

### 2.通过类名来查找

cheeses = driver.find_elements_by_class_name("cheese")
cheeses = driver.find_elements(By.CLASS_NAME, "cheese")

### 3.通过name属性查找

driver.find_elements_by_name("email")
driver.find_elements(By.NAME,'email')

### 4.通过标签名查找

driver.find_elements_by_tag_name('div')
driver.find_elements(By.TAG_NAME,'kw')

### 5.通过xpath 语法查找

driver.find_elements_by_xpath("//div")
driver.find_elements(By.XPATH,'//div')

### 6.通过css选择器选择元素

driver.find_elements_by_css_selector("//div")
driver.find_elements(By.CSS_SELECTOR,'//div')

find_element  获取第一个满足条件的元素
find_elements 获取所有满足条件的元素

## 表单元素操作

```bash
1.button 
input[type='submit']
2.checkbox  
input[type='checkbox ']
3.select 下拉列表
-----------
input_tag=driver.find_element_by_id('kw')
input_tag.send_keys("onion")  #填充
input_tag.clear()  #清除
-----------
remember_tag = driver.find_element_by_id('rememberME')
remember_tag.click()  #点击 
-------------------
```

## 选择标签

```bash
选择select ： select 元素不能直接点击。因为点击后还需要选中元素
<select> </select>

# 导入 Select 类
from selenium.webdriver.support.ui import Select

#找到 name 的选项卡
select_tag = Select(driver.find_element_by_name('status'))

select_tag.select_by_index(1) #索引
select_tag.select_by_value("0") #根据value里的值
select_tag.select_by_visible_text("广播") #根据文本内容
select_tag.deselect_all()  #取消所有的选中
 ```
