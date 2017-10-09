---
title: "Azure Media Indexer에 대해 미리 설정 된 aaaTask"
description: "이 항목에서는 Azure Media Indexer의 미리 설정된 작업 개요를 제공합니다."
services: media-services
documentationcenter: 
author: Asolanki
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: adsolank;juliako;
ms.openlocfilehash: ca0b3e7aa9f6dd9fdecddfc5b3137281ed5cef35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="task-preset-for-azure-media-indexer"></a>Azure Media Indexer의 미리 설정된 작업

Azure Media Indexer는 tooperform hello 다음 작업을 사용 하는 미디어 프로세서: 미디어 파일 및 콘텐츠를 검색할 수 있도록 설정, 닫힌된 캡션 트랙 및 키워드를 생성, 하면 자산의 일부인 자산 파일입니다.

이 항목에서는 hello 설명 태스크 toopass tooyour 인덱싱 작업 해야 하는 기본 설정 합니다. 완전한 예제는 [Azure Media Indexer를 사용하여 미디어 파일 인덱싱](media-services-index-content.md)을 참조하세요.

## <a name="azure-media-indexer-configuration-xml"></a>Azure Media Indexer 구성 XML

hello 다음 표에서 hello 구성 XML의 요소와 특성.

|이름|필요|설명|
|---|---|---|
|입력|true|자산 파일 tooindex 되도록 합니다.<br/>Azure Media Indexer 원하는 미디어 파일 확장명 따르는 hello: MP4, MOV, WMV, MP3, M4A, WMA, AAC, WAV 합니다. <br/><br/>Hello에 hello 파일 이름 (s)을 지정할 수 있습니다 **이름** 또는 **목록** hello 특성 **입력** 요소 중 (아래 참조). 자산 파일 tooindex를 지정 하지 않으면 hello 기본 파일이 선택 됩니다. 기본 자산 파일이 없습니다. 설정 된 경우 hello hello 입력된 자산의 첫 번째 파일이 인덱싱됩니다.<br/><br/>tooexplicitly는 hello 자산 파일 이름 지정을 수행 합니다.<br/>```<input name="TestFile.wmv" />```<br/><br/>여러 자산 파일을 한 번에 (too10 파일을)를 인덱싱할 수 있습니다. toodo이:<br/>- 텍스트 파일(매니페스트 파일)을 만들고 .lst 확장명을 지정합니다.<br/>-모든 hello 자산 파일 이름 목록이 입력된 자산 toothis 매니페스트 파일에 추가 합니다.<br/>-(업로드) 매니페스트 파일 toohello 자산을 추가 합니다.<br/>-Hello 입력의 목록 특성에서 hello 매니페스트 파일의 hello 이름을 지정 합니다.<br/>```<input list="input.lst">```<br/><br/>**참고:** hello 인덱싱 작업이 hello 2006 오류 코드로 실패 10 개 이상의 파일 toohello 매니페스트 파일을 추가 합니다.|
|metadata|false|Hello에 대 한 메타 데이터는 자산 파일을 지정 합니다.<br/>```<metadata key="..." value="..." />```<br/><br/>미리 정의된 키의 값을 제공할 수 있습니다. <br/><br/>현재 키 뒤 hello 지원 됩니다.<br/><br/>**제목** 및 **설명** -tooupdate hello 언어 모델 tooimprove 음성 인식 정확도 사용 합니다.<br/>```<metadata key="title" value="[Title of hello media file]" /><metadata key="description" value="[Description of hello media file]" />```<br/><br/>**username** 및 **password** - http 또는 https를 통해 인터넷 파일을 다운로드할 때 인증에 사용됩니다.<br/>```<metadata key="username" value="[UserName]" /><metadata key="password" value="[Password]" />```<br/>hello 사용자 이름 및 암호 값 hello 입력 매니페스트에 tooall 미디어 Url이 적용 됩니다.|
|기능<br/><br/>버전 1.2에 추가되었습니다. 현재 hello만 지원 기능은 음성 인식 ("ASR")입니다.|false|hello 음성 인식 기능에는 다음 설정 키 hello에 있습니다.<br/><br/>언어:<br/>-hello 자연어 toobe hello 멀티미디어 파일에서 인식 합니다.<br/>- English, Spanish<br/><br/>CaptionFormats:<br/>-hello 목록을 세미콜론으로 구분 하 여 원하는 출력 캡션 형식 (있는 경우)<br/>- ttml;sami;webvtt<br/><br/><br/>GenerateAIB:<br/>-부울 플래그 AIB 파일이 필요한 (SQL Server 및 hello 고객 Indexer IFilter 함께 사용) 인지 여부를 지정 합니다. 자세한 내용은 Using AIB Files with Azure Media Indexer and SQL Server(Azure Media Indexer 및 SQL Server에서 AIB 파일 사용)를 참조하세요.<br/>- True, False<br/><br/>GenerateKeywords:<br/>- 키워드 XML 파일이 필요한지를 지정하는 부울 플래그<br/>- True, False|

## <a name="azure-media-indexer-configuration-xml-example"></a>Azure Media Indexer 구성 XML 예제

``` 
<?xml version="1.0" encoding="utf-8"?>  
<configuration version="2.0">  
  <input>  
    <metadata key="title" value="[Title of hello media file]" />  
    <metadata key="description" value="[Description of hello media file]" />  
  </input>  
  <settings>  
  </settings>  
  
  <features>  
    <feature name="ASR">    
      <settings>  
        <add key="Language" value="English"/>  
        <add key="CaptionFormats" value="ttml;sami;webvtt"/>  
        <add key="GenerateAIB" value ="true" />  
        <add key="GenerateKeywords" value ="true" />  
      </settings>  
    </feature>  
  </features>  
  
</configuration>  
```
  
## <a name="next-steps"></a>다음 단계

[Azure Media Indexer를 사용하여 미디어 파일 인덱싱](media-services-index-content.md)을 참조하세요.

