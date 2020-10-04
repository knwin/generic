# How to's in GScript

### How to add a menu
```
function onOpen() {
  
  var spreadsheet = SpreadsheetApp.getActiveSpreadsheet();
  var entries = [{
    name : "Do This",
    functionName : "doThisFunctionName"
  }];
  
  
  spreadsheet.addMenu("My Menu", entries);
};
```

### Read ESRI service url
modified from https://gist.github.com/varun-raj/5350595a730a62ca1954
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
  var headers = data = Object.keys(dataSet[0].attributes); 
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

### get token from AGOL for REST API
```
function getToken() {
  var source = SpreadsheetApp.getActiveSpreadsheet();//self
  var settingSheet = source.getSheetByName("Settings"); 
  
  
  var formData = {
    'client_id': 'my_client_id',
    'client_secret': 'my_client_secrete',
    'grant_type': 'client_credentials'
  };
  
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

### add features to a Hosted Feature Layer on AGOL
```
  function addFeature(){
        var milliseconds = new Date(date).getTime(); 
        var data = [
                    {
                      "geometry" : {
                        "x": 0,
                        "y": 0,
                        "spatialReference": {
                          "wkid": 4326
                        }
                      },
                      "attributes" : {
                        "Last_Update" : milliseconds,
                        "Confirmed_total" : sourceData[0][1],
                        "Death_total":sourceData[0][2],
                        "Recovered_total":sourceData[0][3],
                        "New_cases":sourceData[0][4],
                        "New_deaths":sourceData[0][5],
                        "New_recovered":sourceData[0][6],
                        "Lat":0,
                        "Lon":0
                      }
                    }
                  ];
        data = JSON.stringify(data);
        var token = getToken();          
        
        var requestOptions = {
          method: 'POST',
          headers: myHeaders,
          payload: 'f=json&token='+token+'&adds='+data,
          redirect: 'follow'
        };
        
        UrlFetchApp.fetch(url, requestOptions);

 };
```

### Delete featues
```
function deleteFeatures(token, objectId_list){

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
