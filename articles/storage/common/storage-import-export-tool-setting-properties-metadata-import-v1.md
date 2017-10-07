---
title: "aaaSetting 속성 및 메타 데이터 Azure 가져오기/내보내기-v 1을 사용 하 여 | Microsoft Docs"
description: "Hello Azure 가져오기/내보내기 도구 tooprepare 드라이브를 실행할 때 toospecify 속성 및 메타 데이터 toobe hello 대상 blob에 대 한 설정 방법에 대해 알아봅니다. 이 toov1의 hello 가져오기/내보내기 도구를 가리킵니다."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: e8541695-bcfb-4bf0-84d9-72c9de32a0a8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 5b7b1c346ecde8a26d985bd5de7efcf7d86eb9e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-properties-and-metadata-during-hello-import-process"></a>속성 설정 및 hello 중에 메타 데이터 가져오기 프로세스
Microsoft Azure 가져오기/내보내기 도구 tooprepare hello 드라이브를 실행 하면 속성 및 메타 데이터 toobe hello 대상 blob에 대 한 설정에 지정할 수 있습니다. 다음 단계를 수행하세요.  
  
1.  tooset blob 속성, 속성 이름 및 값을 지정 하는 로컬 컴퓨터에 텍스트 파일을 만듭니다.  
  
2.  tooset blob 메타 데이터, 메타 데이터 이름 및 값을 지정 하는 로컬 컴퓨터에 텍스트 파일을 만듭니다.  
  
3.  Hello 전체 경로 tooone 중 또는 둘 다 이러한 파일 toohello Azure 가져오기/내보내기 도구 hello의 일부로 전달 `PrepImport` 작업 합니다.  
  
> [!NOTE]
>  속성 또는 메타데이터 파일을 복사 세션의 일부로 지정하면 해당 복사 세션의 일부로 가져오는 모든 Blob에 대해 해당 속성 또는 메타데이터가 설정됩니다. 가져올 hello blob 중 일부에 대해 toospecify 다양 한 속성이 나 메타 데이터를 원하는 toocreate 별도 세션 다른 속성이 나 메타 데이터 파일을 복사 해야 합니다.  
  
## <a name="specify-blob-properties-in-a-text-file"></a>텍스트 파일에서 Blob 속성 지정  
toospecify blob 속성 로컬 텍스트 파일을 만들고으로 요소 및 속성 값을 값으로 속성 이름을 지정 하는 XML을 포함 합니다. 다음은 몇 가지 속성 값을 지정하는 예입니다.  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
Hello 파일 tooa와 같은 로컬 위치에 저장 `C:\WAImportExport\ImportProperties.txt`합니다.  
  
## <a name="specify-blob-metadata-in-a-text-file"></a>텍스트 파일에서 Blob 메타데이터를 지정합니다.  
마찬가지로, toospecify blob 메타 데이터, 메타 데이터 이름으로 요소 및 메타 데이터 값을 값으로 지정 하는 로컬 텍스트 파일을 만듭니다. 다음은 몇 가지 메타데이터 값을 지정하는 예입니다.  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
Hello 파일 tooa와 같은 로컬 위치에 저장 `C:\WAImportExport\ImportMetadata.txt`합니다.  
  
## <a name="create-a-copy-session-including-hello-properties-or-metadata-files"></a>포함 하 여 복사 세션 hello 속성 또는 메타 데이터 파일 만들기  
Hello Azure 가져오기/내보내기 도구 tooprepare hello 가져오기 작업을 실행 하면 hello를 사용 하 여 hello 명령줄에서 hello 속성 파일을 지정 합니다. `PropertyFile` 매개 변수입니다. Hello를 사용 하 여 hello 명령줄에서 hello 메타 데이터 파일을 지정 `/MetadataFile` 매개 변수입니다. 다음은 두 파일을 지정하는 예입니다.  
  
```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```
  
## <a name="next-steps"></a>다음 단계

* [가져오기-내보내기 서비스 메타데이터 및 속성 파일 형식](../storage-import-export-file-format-metadata-and-properties.md)
