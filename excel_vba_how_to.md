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
If all the slicer are seleted as False, it will reselect all slicer and therefore one slicer is made selected in each loop

### Exporting charts with slicer
'https://stackoverflow.com/questions/11939087/export-chart-as-image-with-click-of-a-button

with slicer on pivot table and chart from pivot data
```
Sub SliceAndSaveChart()
Dim myChart As Chart

Set myChart = ActiveWorkbook.Charts(1)
myChart.Refresh
s_count = ActiveWorkbook.SlicerCaches("Slicer_village").SlicerItems.Count

ActiveWorkbook.SlicerCaches("Slicer_village").SlicerItems(1).Selected = True
'make sure other slicers are deselected
For i = 2 To s_count
    ActiveWorkbook.SlicerCaches("Slicer_village").SlicerItems(i).Selected = False
Next
'file_name = ActiveWorkbook.SlicerCaches("Slicer_village").SlicerItems(1).Value & "_chart.png"
'myChart.Export Filename:=ThisWorkbook.Path & "\" & file_name, FilterName:="PNG"

For i = 1 To s_count

    If i > 1 Then
       ActiveWorkbook.SlicerCaches("Slicer_village").SlicerItems(i).Selected = True
       ActiveWorkbook.SlicerCaches("Slicer_village").SlicerItems(i - 1).Selected = False
    End If
   file_name = ActiveWorkbook.SlicerCaches("Slicer_village").SlicerItems(i).Value & "_chart.png"
   Set myChart = ActiveWorkbook.Charts(1)
   myChart.Refresh

   Application.Wait Now + #12:00:01 AM#
   myChart.Export Filename:=ThisWorkbook.Path & "\" & file_name, FilterName:="PNG"
   'reset
   Set myChart = Nothing
Next i

End Sub
```

### Exporting sliced pivot tables as picture
modified from https://www.reddit.com/r/excel/comments/954t17/selecting_a_pivot_table_and_saving_it_as_an_image/

```
Sub SliceAndSaveTableAsPicture()

ActiveWorkbook.SlicerCaches("Slicer_village").SlicerItems(1).Selected = True

'make sure other slicers are deselected
s_count = ActiveWorkbook.SlicerCaches("Slicer_village").SlicerItems.Count
For i = 2 To s_count
    ActiveWorkbook.SlicerCaches("Slicer_village").SlicerItems(i).Selected = False
Next

For i = 1 To s_count
    If i > 1 Then
        ActiveWorkbook.SlicerCaches("Slicer_village").SlicerItems(i).Selected = True
        ActiveWorkbook.SlicerCaches("Slicer_village").SlicerItems(i - 1).Selected = False
    End If
    
    file_name = ActiveWorkbook.SlicerCaches("Slicer_village").SlicerItems(i).Value & "_table.png"

    'Create temporary chart as canvas
    ActiveSheet.PivotTables(1).PivotSelect "", xlDataAndLabel, True
    
    Set sht = Selection.Worksheet
    Selection.Copy
    DoEvents
    Application.Wait Now + #12:00:01 AM#
    sht.Pictures.Paste.Select
    
    Set sh = sht.Shapes(sht.Shapes.Count)
    sh.Width = sh.Width * 2
    sh.Height = sh.Height * 2
    Set tmpChart = Charts.Add
    
    tmpChart.ChartArea.Clear
    
    tmpChart.Name = "PicChart" & (Rnd() * 10000)
    
    Set tmpChart = tmpChart.Location(Where:=xlLocationAsObject, Name:=sht.Name)
    
    tmpChart.ChartArea.Width = sh.Width
    tmpChart.ChartArea.Height = sh.Height
    tmpChart.Parent.Border.LineStyle = 0
    
    'Paste range as image to chart
    
    sh.Copy
    
    tmpChart.ChartArea.Select
    Application.Wait Now + #12:00:01 AM#
    
    tmpChart.Paste    
    
    'Save chart image to file    
    tmpChart.Export Filename:=file_name, FilterName:="png"
        
    DoEvents
    
    ActiveSheet.PivotTables(1).PivotSelect "", xlDataAndLabel, True
    
    sht.Cells(1, 1).Activate
    
    sht.ChartObjects(sht.ChartObjects.Count).Delete
    
    sh.Delete

    ActiveSheet.PivotTables(1).PivotSelect "", xlDataAndLabel, False
   
Next i

End Sub
```
