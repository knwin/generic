### How to get unique items from a range
```
Dim unique_itmes() As String
my_range = Range(RefEdit)
tmp = ""
For i = 1 To my_range.Cells.Count    
    item_i = my_range(i)
    If (InStr(tmp, item_i = 0) Then
        tmp = tmp & item_i & "|"
    End If   
Next i
tmp = left(tmp,len(tmp)-1
unique_items = Split(tmp, "|")
```

### How to get actual data range from selected columns (with RefEdit control)
```
range_text  = RefEdit1.Value
If InStr(1, range_text , ":") Then
    range_start = Split(range_text, ":")(0)
    range_end = Split(range_text, ":")(1)
    sheet_name = Split(range_start, "!")(0)
    range_start = Split(range_start, "!")(1)
    
    col_count = Range(range_text).Column
    
    hasRowNumber = InStr(2, range_end, "$")
    If hasRowNumber = 0 Then
        last_row = 1
        For I = 0 To col_count
            tmp_row = Range(range_start & 65000).Offset(0, I).End(xlUp).Row
            
            If last_row < tmp_row Then last_row = tmp_row

        Next
        first_row = 1
        For I = 0 To col_count
            tmp_row = Range(range_start & 1).Offset(0, I).End(xlUp).Row
            If first_row < tmp_row Then first_row = tmp_row
        Next I
        
        range_start = range_start & "$" & first_row
        range_end = range_end & "$" & last_row
    End If
    range_text = sheet_name & "!" & range_start & ":" & range_end
End If

```

### How to save copy as
```
ActiveWorkbook.SaveCopyAs(file_name)

```

### How to save chart
```
Dim myChart As Chart
Set myChart = ActiveWorkbook.Charts(index)
file_name = "my_chart.png"
myChart.Export Filename:=ThisWorkbook.Path & "\" & file_name, Filtername:="PNG"
```

### Loop slicers
```
s_count = ActiveWorkbook.SlicerCaches("Slicer_village").SlicerItems.Count

`deselect all slicer except 1st one
ActiveWorkbook.SlicerCaches("Slicer_village").SlicerItems(1).Selected = True
For i = 2 To s_count
    ActiveWorkbook.SlicerCaches("Slicer_village").SlicerItems(i).Selected = False
Next
file_name = ActiveWorkbook.SlicerCaches("Slicer_village").SlicerItems(1).Value & ".xlsx"
ActiveWorkbook.SaveCopyAs (file_name)

`change slicers and save copy as new files
For i = 2 To s_count

   ActiveWorkbook.SlicerCaches("Slicer_village").SlicerItems(i).Selected = True
   ActiveWorkbook.SlicerCaches("Slicer_village").SlicerItems(i-1).Selected = False
   file_name = ActiveWorkbook.SlicerCaches("Slicer_village").SlicerItems(i).Value & ".xlsx"
   ActiveWorkbook.SaveCopyAs (file_name)

Next i

```
If all the slicer are Seleted as False, it will sell all slicer and therefore one slicer is made selected in each loop
