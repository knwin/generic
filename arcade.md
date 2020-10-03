# Useful Arcade Expressions

### convert to Myanmar number in List Item
```
var value1 = $datapoint["Filed_Name1"];
var value2 = $datapoint["Filed_Name2"];
var value3 = $datapoint["Filed_Name3"];

var num = ["၀","၁","၂","၃","၄","၅","၆","၇","၈","၉"];
for (var i = 0; i < 10; i++ ){   
    value1 = replace(value1, i, num[i]);  
    value2 = replace(value2, i, num[i]); 
    value3 = replace(value3, i, num[i]); 
};
return {
  attributes: {
    attrib1: value1,
    attrib2: value2,
    attrib3: value3
  }
}
```

### convert to Myanmar number in Indicator Item
```
var value1 = $datapoint["Filed_Name1"];
var value2 = $datapoint["Filed_Name2"];
var value3 = $datapoint["Filed_Name3"];

var num = ["၀","၁","၂","၃","၄","၅","၆","၇","၈","၉"];
for (var i = 0; i < 10; i++ ){   
    value1 = replace(value1, i, num[i]);  
    value2 = replace(value2, i, num[i]); 
    value3 = replace(value3, i, num[i]); 
};
return {
    middleText: value1 + ' (' + value2 + ')',
    middleTextColor: '#ff0000',
    bottomText: '(ယနေ့ထပ်တိုး '+ value3+')',
}
```
### convert to Myanmar Admin names in a List Itme
```
var ts_mya_list = {"Ahlone Township":"အလုံ",
    "Amarapura Township":"အမရပူရ",
    "Bago Township":"ပဲခူး",
    "Zay Yar Thi Ri Township":"ဇေယျာသီရိ"
};
var ts_name = $datapoint["Township"];
var ts_mya_name = ts_mya_list[ts_name];
var confirmed = $datapoint.Confirmed;
return {
   attributes: {
    ts_mya: ts_mya_name,
  }
}
```
in the list template use ```{expression/ts_mya}``` to get the value

### Convert to Myanmar Admin names in the Map Popup and Label
Open Configure Pop-up menu and add as new expression

```
var ts_mya_list = {"Ahlone Township":"အလုံ",
"Amarapura Township":"အမရပူရ",
"Bago Township":"ပဲခူး",
"Zay Yar Thi Ri Township":"ဇေယျာသီရိ"
};
var ts_name = $datapoint["Township"];
var ts_mya_name = ts_mya_list[ts_name];
var confirmed = $datapoint.Confirmed;
return {ts_mya[$feature["Township"]]);
```
Pop-up - although variable name is appeared in the attribute list, actual usage will be {expression/expr#}

Label - variable name will be appeared in the field list
