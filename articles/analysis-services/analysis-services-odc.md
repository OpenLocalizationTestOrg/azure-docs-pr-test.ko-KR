---
title: ".odc 파일 tooconnect tooan Azure Analysis Services 서버 aaaCreate | Microsoft Docs"
description: "Office 데이터 연결 파일 tooconnect tooand toocreate Azure에서 Analysis Services 서버에서 데이터를 가져오기 하는 방법에 대해 알아봅니다."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/23/2017
ms.author: owend
ms.openlocfilehash: 9c8c8df23b17f19905d7ec51af4eb63eb995045e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-office-data-connection-file"></a>Office 데이터 연결 파일 만들기

이 문서에서는 버전 번호 16.0.7369.2117 Excel 2016에서 Office 데이터 연결 파일 tooconnect tooan Azure Analysis Services 서버를 만드는 방법을 설명 또는 이전 버전에서는 또는 Excel 2013. 업데이트된 [MSOLAP.7 공급자](analysis-services-data-providers.md)도 필요합니다.


1. 아래의 hello 샘플 연결 파일을 복사 하 고 텍스트 편집기에 붙여 넣습니다. 

2. `odc:ConnectionString`, hello 다음과 같은 속성을 변경 합니다.

    *   `Data Source=asazure://<region>.asazure.windows.net/<servername>;` 변경 `<region>` Analysis Services 서버의 toohello 영역 및 `<servername>` toohello 서버 이름입니다.

    *   `Initial Catalog=<database>;` 변경 `<database>` toohello 데이터베이스 이름입니다.

3. `<odc:CommandText>Model</odc:CommandText>` 변경 `Model` 모델이 나 큐브 뷰의의 toohello 이름입니다. 

4. Hello 파일을 저장 한 `.odc` 확장 toohello C:\Users\\*username*\Documents\My 데이터 원본 폴더입니다.

5. Hello 파일을 마우스 오른쪽 단추로 누른 **Excel에서 열기**합니다. 또는 Excel hello에 **데이터** 리본에서 클릭 **기존 연결**프로그램 파일을 선택한 다음 클릭 **열려**합니다.



**샘플 연결 파일**
```
<html xmlns:o="urn:schemas-microsoft-com:office:office"
xmlns="http://www.w3.org/TR/REC-html40">

<head>
<meta http-equiv=Content-Type content="text/x-ms-odc; charset=utf-8">
<meta name=ProgId content=ODC.Cube>
<meta name=SourceType content=OLEDB>
<meta name=Catalog content="Database">
<meta name=Table content=Model>
<title>AzureAnalysisServicesConnection</title>
<xml id=docprops><o:DocumentProperties
  xmlns:o="urn:schemas-microsoft-com:office:office"
  xmlns="http://www.w3.org/TR/REC-html40">
  <o:Name>SampleAzureAnalysisServices</o:Name>
 </o:DocumentProperties>
</xml><xml id=msodc><odc:OfficeDataConnection
  xmlns:odc="urn:schemas-microsoft-com:office:odc"
  xmlns="http://www.w3.org/TR/REC-html40">
  <odc:Connection odc:Type="OLEDB">
   <odc:ConnectionString>Provider=MSOLAP.7;Data Source=asazure://<region>.asazure.windows.net/<servername>;Initial Catalog=<database>;</odc:ConnectionString>
   <odc:CommandType>Cube</odc:CommandType>
   <odc:CommandText>Model</odc:CommandText>
  </odc:Connection>
 </odc:OfficeDataConnection>
</xml>
<style>
<!--
    .ODCDataSource
    {
    behavior: url(dataconn.htc);
    }
-->
</style>
 
</head>

<body onload='init()' scroll=no leftmargin=0 topmargin=0 rightmargin=0 style='border: 0px'>
<table style='border: solid 1px threedface; height: 100%; width: 100%' cellpadding=0 cellspacing=0 width='100%'> 
  <tr> 
    <td id=tdName style='font-family:arial; font-size:medium; padding: 3px; background-color: threedface'> 
      &nbsp; 
    </td> 
     <td id=tdTableDropdown style='padding: 3px; background-color: threedface; vertical-align: top; padding-bottom: 3px'>

      &nbsp; 
    </td> 
  </tr> 
  <tr> 
    <td id=tdDesc colspan='2' style='border-bottom: 1px threedshadow solid; font-family: Arial; font-size: 1pt; padding: 2px; background-color: threedface'>

      &nbsp; 
    </td> 
  </tr> 
  <tr> 
    <td colspan='2' style='height: 100%; padding-bottom: 4px; border-top: 1px threedhighlight solid;'> 
      <div id='pt' style='height: 100%' class='ODCDataSource'></div> 
    </td> 
  </tr> 
</table> 

  
<script language='javascript'> 

function init() { 
  var sName, sDescription; 
  var i, j; 
  
  try { 
    sName = unescape(location.href) 
  
    i = sName.lastIndexOf(".") 
    if (i>=0) { sName = sName.substring(1, i); } 
  
    i = sName.lastIndexOf("/") 
    if (i>=0) { sName = sName.substring(i+1, sName.length); } 

    document.title = sName; 
    document.getElementById("tdName").innerText = sName; 

    sDescription = document.getElementById("docprops").innerHTML; 
  
    i = sDescription.indexOf("escription>") 
    if (i>=0) { j = sDescription.indexOf("escription>", i + 11); } 

    if (i>=0 && j >= 0) { 
      j = sDescription.lastIndexOf("</", j); 

      if (j>=0) { 
          sDescription = sDescription.substring(i+11, j); 
        if (sDescription != "") { 
            document.getElementById("tdDesc").style.fontSize="x-small"; 
          document.getElementById("tdDesc").innerHTML = sDescription; 
          } 
        } 
      } 
    } 
  catch(e) { 

    } 
  } 
</script> 

</body> 
 
</html>

```



