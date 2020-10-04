# How to's in GScript

### How to add a function to a menu
```
function onOpen() {
  
  var spreadsheet = SpreadsheetApp.getActiveSpreadsheet();
  var entries = [{
    name : "My Function",
    functionName : "myFunctionName"
  }];
  spreadsheet.addMenu("My Menu", entries);
};
```

### Get token from AGOL for REST API
```
function getToken() {
  var source = SpreadsheetApp.getActiveSpreadsheet();//self
  var settingSheet = source.getSheetByName("Settings"); 
  
  var formData = {
    'client_id': 'my_client_id',
    'client_secret': 'my_client_secrete',
    'grant_type': 'client_credentials'
  }; 
  // read detail in https://developers.arcgis.com/labs/rest/get-an-access-token/
  
  var options = {
    'method' : 'post',
    'payload' : formData
  };
  var response = UrlFetchApp.fetch('https://www.arcgis.com/sharing/rest/oauth2/token', options);
  var json = response.getContentText();
  var data = JSON.parse(json);
  return (data.access_token);
}
```

### Add features to a Hosted Feature Layer on AGOL
```
  var url = "https://services8.arcgis.com/XXXXXXXX/arcgis/rest/services/FFFFFF/FeatureServer/0/applyEdits";
  function addFeature(url){
        var data = [
                    {
                      "geometry" : {
                        "x": 12.00,
                        "y": 90.00,
                        "spatialReference": {
                          "wkid": 4326
                        }
                      },
                      "attributes" : {
                        "Field1" : field1_value,
                        "Field2" : sourceData[0][1],
                        "Field":sourceData[0][2],
                      }
                    }
                  ];
        data = JSON.stringify(data);
        var token = getToken();          
        var myHeaders = { 'Content-Type': 'application/x-www-form-urlencoded'};
        var requestOptions = {
          method: 'POST',
          headers: myHeaders,
          payload: 'f=json&token='+token+'&adds='+data,
          redirect: 'follow'
        };
        
        UrlFetchApp.fetch(url, requestOptions);

 };
```

### Delete features
```
var url = "https://services8.arcgis.com/XXXXXXXX/arcgis/rest/services/FFFFFF/FeatureServer/0/applyEdits";
function deleteFeatures(token, objectId_list, url){

  var myHeaders = { 'Content-Type': 'application/x-www-form-urlencoded'};    
  var objects_tobe_deleted = JSON.stringify(objectId_list);  
  var requestOptions = {
    method: 'POST',
    headers: myHeaders,
    payload: 'f=json&token='+token+'&deletes='+objects_tobe_deleted,
    redirect: 'follow'
  };
  
  UrlFetchApp.fetch(url, requestOptions);
}
```


### Read attributes of a hosted feature layer via ESRI service url and add into a sheet
below code is modified from https://gist.github.com/varun-raj/5350595a730a62ca1954
```
function pullJSON() {
  var ss = SpreadsheetApp.getActiveSpreadsheet();
  var sheet = ss.getActiveSheet();
  
  var refSheet = ss.getSheetByName("Ref"); // sheet name with url string
  var url = refSheet.getRange("B2").getValue(); // cell with url string

  var response = UrlFetchApp.fetch(url); // get feed
  var dataAll = JSON.parse(response.getContentText()); //
  var dataSet = dataAll.features;
  
  var rows = [],
      data;
      
  // get keys as column names
  var headers = Object.keys(dataSet[0].attributes); 
  rows.push(headers);
  
  // get values of attributes object
  for (i = 0; i < dataSet.length; i++) {
    data = Object.values(dataSet[i].attributes); 
    rows.push(data); 
  }

  dataRange = sheet.getRange(4, 1, rows.length, data.length); // data.length makesure exact number of columns
  dataRange.setValues(rows);
}
```

