# JS如何读取表单值
1. 从多选的<select>元素中读取值：
   对于<select multiple>元素，你需要遍历所有的选项（<option>），并检查每个选项的selected属性是否为true来判断该选项是否被选中。

```javascript
// 获取<select>元素
var selectElement = document.getElementById("mySelect");

// 存储选中的选项值
var selectedValues = [];

// 遍历<select>中的所有<option>
for (var i = 0; i < selectElement.options.length; i++) {
if (selectElement.options[i].selected) {
selectedValues.push(selectElement.options[i].value);
}
}

// 现在selectedValues数组包含了所有选中的选项的值
```
2. 从一组复选框中读取值：
   如果你有一组复选框，并希望获取所有被选中的复选框的值，你同样需要遍历它们并检查它们的checked属性。

```javascript
// 获取所有具有相同名称的复选框的集合
var checkboxes = document.querySelectorAll('input[name="myCheckbox"]:checked');

// 存储选中的复选框值
var checkedValues = [];

// 遍历所有选中的复选框并获取它们的值
checkboxes.forEach(function(checkbox) {
checkedValues.push(checkbox.value);
});

// 现在checkedValues数组包含了所有选中的复选框的值
```
在上述代码中，document.querySelectorAll('input[name="myCheckbox"]:checked')会选择所有名为"myCheckbox"并且被选中的复选框。

读取多项选择的值时，重要的是要确保你遍历的是正确的元素集合，并且正确地检查它们的选择状态（selected对于<option>元素，checked对于复选框）。使用数组来存储这些选中的值是一种常见的做法，因为它允许你轻松地访问和使用这些值。



```
function formSubmit() {
// TODO：待补充代码
const quescontent = document.getElementById("quescontent");
const result = document.getElementById("result");
const weight = document.getElementById("weight").value;
const height = document.getElementById("height").value;
const male = document.querySelector('[type="radio"]:checked').value;
const place = document.querySelectorAll('[name="place"]:checked');
const placeArr = [];
place.forEach((el) => placeArr.push(el.nextSibling.textContent.trim()));
const res = `身高${height}cm，体重${weight}kg，性别 ${
male == 0 ? "男" : "女"
}，会在${[...placeArr]}健身锻炼`;
result.innerHTML += `<br> ${res}`;
quescontent.style.display = "none";
result.style.display = "block";
}
```
