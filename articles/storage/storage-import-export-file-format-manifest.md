---
title: "aaaAzure 가져오기/내보내기 매니페스트 파일 형식 | Microsoft Docs"
description: "Azure Blob 저장소의 blob 및 hello 가져오기/내보내기 서비스에서 가져오기 또는 내보내기 작업의 드라이브에서 파일 간의 hello 매핑을 설명 하는 hello 드라이브 매니페스트 파일의 hello 형식에 알아봅니다."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: f3119e1c-2c25-48ad-8752-a6ed4adadbb0
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: d7e5e1990482916f7ff5f891c97343b52e82b2f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-manifest-file-format"></a>Azure Import/Export 서비스 매니페스트 파일 형식
hello 드라이브 매니페스트 파일에는 Azure Blob 저장소에서 blob과 가져오기 또는 내보내기 작업으로 구성 된 드라이브에 파일 간의 hello 매핑을 설명 합니다. 가져오기 작업에 대 한 hello 매니페스트 파일 hello 드라이브 준비 프로세스의 일부로 만들어지고 hello 드라이브 toohello Azure 데이터 센터로 전송 되기 전에 hello 드라이브에 저장 됩니다. 내보내기 작업 중 hello 매니페스트 생성 되어 hello Azure 가져오기/내보내기 서비스에서 hello 드라이브에 저장 합니다.  
  
둘 다 가져오기 및 내보내기 작업 hello 드라이브 매니페스트 파일 저장에 대 한 hello에 가져오기 또는 내보내기 드라이브; 없으면 toohello 서비스 API 작업을 통해 전송 합니다.  
  
hello 다음 드라이브 매니페스트 파일의 일반 형식은 hello를 설명합니다.  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveManifest Version="2014-11-01">  
  <Drive>  
    <DriveId>drive-id</DriveId>  
    import-export-credential  
  
    <!-- First Blob List -->  
    <BlobList>  
      <!-- Global properties and metadata that applies tooall blobs -->  
      [<MetadataPath Hash="md5-hash">global-metadata-file-path</MetadataPath>]  
      [<PropertiesPath   
        Hash="md5-hash">global-properties-file-path</PropertiesPath>]  
  
      <!-- First Blob -->  
      <Blob>  
        <BlobPath>blob-path-relative-to-account</BlobPath>  
        <FilePath>file-path-relative-to-transfer-disk</FilePath>  
        [<ClientData>client-data</ClientData>]  
        [<Snapshot>snapshot</Snapshot>]  
        <Length>content-length</Length>  
        [<ImportDisposition>import-disposition</ImportDisposition>]  
        page-range-list-or-block-list          
        [<MetadataPath Hash="md5-hash">metadata-file-path</MetadataPath>]  
        [<PropertiesPath Hash="md5-hash">properties-file-path</PropertiesPath>]  
      </Blob>  
  
      <!-- Second Blob -->  
      <Blob>  
      . . .  
      </Blob>  
    </BlobList>  
  
    <!-- Second Blob List -->  
    <BlobList>  
    . . .  
    </BlobList>  
  </Drive>  
</DriveManifest>  
  
import-export-credential ::=   
  <StorageAccountKey>storage-account-key</StorageAccountKey> | <ContainerSas>container-sas</ContainerSas>  
  
page-range-list-or-block-list ::=   
  page-range-list | block-list  
  
page-range-list ::=   
    <PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       Hash="md5-hash"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       Hash="md5-hash"/>]  
    </PageRangeList>  
  
block-list ::=  
    <BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       Hash="md5-hash"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       Hash="md5-hash"/>]  
    </BlockList>  

```

## <a name="manifest-xml-elements-and-attributes"></a>매니페스트 XML 요소 및 특성

hello 드라이브 매니페스트 XML 형식의의 hello 데이터 요소와 특성은 다음 표에 hello에 지정 됩니다.  
  
|XML 요소|형식|설명|  
|-----------------|----------|-----------------|  
|`DriveManifest`|루트 요소|hello hello 매니페스트 파일의 루트 요소입니다. Hello 파일의 다른 모든 요소는이 요소 아래에 있습니다.|  
|`Version`|특성, 문자열|hello 매니페스트 파일의 hello 버전입니다.|  
|`Drive`|중첩 XML 요소|각 드라이브에 대 한 hello 매니페스트를 포함합니다.|  
|`DriveId`|문자열|hello hello 드라이브에 대 한 고유 드라이브 식별자입니다. hello 드라이브 식별자를 hello 드라이브 일련 번호에 대 한 쿼리를 통해 찾을 수 있습니다. 드라이브 일련 번호 hello hello 드라이브도 외부 hello에 일반적으로 인쇄 됩니다. hello `DriveID` 하기 전에 나타나야 합니다 `BlobList` hello 매니페스트 파일의 요소입니다.|  
|`StorageAccountKey`|문자열|`ContainerSas`이 지정되지 않은 경우 가져오기 작업에 필요합니다. hello 작업과 연결 된 hello Azure 저장소 계정에 대 한 hello 계정 키입니다.<br /><br /> 이 요소는 내보내기 작업에 대 한 hello 매니페스트에서 생략 됩니다.|  
|`ContainerSas`|문자열|`StorageAccountKey`이 지정되지 않은 경우 가져오기 작업에 필요합니다. hello 작업과 연결 된 hello blob에 액세스 하기 위한 hello 컨테이너 SAS입니다. 참조 [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) 해당 형식에 대 한 합니다. 이 요소는 내보내기 작업에 대 한 hello 매니페스트에서 생략 됩니다.|  
|`ClientCreator`|문자열|Hello을 만든 클라이언트를 hello XML 파일을 지정 합니다. 이 값 hello 가져오기/내보내기 서비스에서 해석 되지 않습니다.|  
|`BlobList`|중첩 XML 요소|부분이 hello 가져오기 또는 내보내기 작업 하는 blob의 목록을 포함 합니다. Blob 목록에 각 blob 공유 hello 같은 메타 데이터 및 속성입니다.|  
|`BlobList/MetadataPath`|문자열|선택 사항입니다. Hello 가져오기 작업에 대 한 hello blob 목록 blob에에서 대해 설정할 수 있는 hello 기본 메타 데이터를 포함 하는 hello 디스크에 있는 파일의 상대 경로 지정 합니다. 이 메타데이터는 Blob 별로 선택적으로 재정의될 수 있습니다.<br /><br /> 이 요소는 내보내기 작업에 대 한 hello 매니페스트에서 생략 됩니다.|  
|`BlobList/MetadataPath/@Hash`|특성, 문자열|Hello 메타 데이터 파일에 대 한 hello Base16 인코딩된 MD5 해시 값을 지정합니다.|  
|`BlobList/PropertiesPath`|문자열|선택 사항입니다. Hello 가져오기 작업에 대 한 hello blob 목록 blob에에서 대해 설정할 수 있는 hello 기본 속성을 포함 하는 hello 디스크에 있는 파일의 상대 경로 지정 합니다. 이러한 속성은 Blob 별로 선택적으로 재정의될 수 있습니다.<br /><br /> 이 요소는 내보내기 작업에 대 한 hello 매니페스트에서 생략 됩니다.|  
|`BlobList/PropertiesPath/@Hash`|특성, 문자열|Hello 속성 파일에 대 한 hello Base16 인코딩된 MD5 해시 값을 지정합니다.|  
|`Blob`|중첩 XML 요소|각 Blob 목록에 있는 각 Blob에 대한 정보를 포함합니다.|  
|`Blob/BlobPath`|문자열|hello 상대 URI toohello blob hello 컨테이너 이름으로 시작 합니다. 로 시작 해야 hello blob이 루트 컨테이너에 있으면, `$root`합니다.|  
|`Blob/FilePath`|문자열|Hello hello 드라이브에 toohello 파일 상대 경로 지정합니다. 내보내기 작업에 대 한 hello blob 경로에 사용할 가능 하면; hello 파일 경로 *예:*, `pictures/bob/wild/desert.jpg` 너무 내보낼`\pictures\bob\wild\desert.jpg`합니다. 그러나 NTFS 이름의 제한 toohello, 기한 blob hello blob 경로 유사 하지 않은 경로 사용 하 여 내보낸된 tooa 파일 수 있습니다.|  
|`Blob/ClientData`|문자열|선택 사항입니다. Hello 고객의 주석이 포함 됩니다. 이 값 hello 가져오기/내보내기 서비스에서 해석 되지 않습니다.|  
|`Blob/Snapshot`|DateTime|내보내기 작업의 경우 선택 사항입니다. 내보낸된 blob 스냅숏에 대 한 hello 스냅숏 식별자를 지정합니다.|  
|`Blob/Length`|Integer|Hello hello blob의 총 길이 바이트 단위로 지정 합니다. hello 값 too200 GB 블록 blob 및 페이지 blob에 대 한 too1 TB를 수 있습니다. 페이지 Blob의 경우 이 값은 512의 배수입니다.|  
|`Blob/ImportDisposition`|문자열|가져오기 작업의 경우 선택 사항이고 내보내기 작업의 경우 생략됩니다. 이 가져오기/내보내기 서비스 hello 처리 방법을 hello 경우 가져오기 작업에 대 한 hello 이미 이름과 같은 이름을 사용 하 여 blob가 존재 하는 위치를 지정 합니다. Hello 기본값은 hello 가져오기 매니페스트에서이 값을 생략 하면 `rename`합니다.<br /><br /> 이 요소에 대 한 hello 값은 다음과 같습니다.<br /><br /> -   `no-overwrite`: 대상 blob가 이미 hello로 있는 경우 이름이 같은 hello 가져오기 작업의 가져오기를 건너뜁니다이 파일입니다.<br />-   `overwrite`: 모든 기존 대상 blob은 완전히 덮어씁니다 hello 새로 가져온된 파일이 있습니다.<br />-   `rename`: 새 blob hello 수정 된 이름으로 업로드 됩니다.<br /><br /> 규칙 이름 바꾸기 hello는 다음과 같습니다.<br /><br /> -추가 하 여 새 이름이 생성 hello blob 이름에 점이 포함 하지 않는 경우 `(2)` toohello 원래 blob 이름에이 새로운 이름을 충돌 하는 기존 blob 이름과 다음 경우 `(3)` 가 대신 추가 `(2)`식입니다.<br />-Hello blob 이름에 점이 있으면, hello 마지막 점 hello 부분은 hello 확장 이름으로 간주 됩니다. 절차, 위 비슷한 toohello `(2)` 앞에 삽입 된 마지막 점 toogenerate 새 이름을 hello; hello 새 이름을 기존 blob 이름과 여전히 충돌, 다음 hello 서비스 시도 `(3)`, `(4)`, 등의 충돌 하지 않는 될 때까지 이름은 찾을 수 있습니다.<br /><br /> 일부 사례:<br /><br /> hello blob `BlobNameWithoutDot` 로 바뀝니다:<br /><br /> `BlobNameWithoutDot (2)  // if BlobNameWithoutDot exists`<br /><br /> `BlobNameWithoutDot (3)  // if both BlobNameWithoutDot and BlobNameWithoutDot (2) exist`<br /><br /> hello blob `Seattle.jpg` 로 바뀝니다:<br /><br /> `Seattle (2).jpg  // if Seattle.jpg exists`<br /><br /> `Seattle (3).jpg  // if both Seattle.jpg and Seattle (2).jpg exist`|  
|`PageRangeList`|중첩 XML 요소|페이지 Blob에 필요합니다.<br /><br /> 가져오기에 대 한 작업을 가져올 파일 toobe의 바이트 범위 목록을 지정 합니다. 각 페이지 범위는 오프셋과 길이 hello 영역의 MD5 해시와 함께 hello 페이지 범위를 설명 하는 hello 소스 파일에 설명 되어 있습니다. hello `Hash` 페이지 범위의 특성이 필요 합니다. hello 서비스는 hello blob 데이터를 hello의 hello 해시 hello 페이지 범위에서 계산 된 hello MD5 해시와 일치 하는지 확인 합니다. 페이지 범위를 개수에 관계 없이 사용 되는 toodescribe too1 TB hello 전체 크기를 사용 하 여 프로그램 가져오기에 대 한 파일 수 있습니다. 오프셋을 기준으로 모든 페이지 범위를 정렬해야 하고 겹치지 않아야 합니다.<br /><br /> 내보내기 작업에 대 한 된 blob의 바이트 범위 집합을 내보낸 toohello 드라이브를 지정 합니다.<br /><br /> 함께 hello 페이지 범위는 blob 또는 파일의 하위 범위에만 넘어갈 수 있습니다.  페이지 범위가 적용 되지 않는 hello 파일의 나머지 부분 hello는 하며 해당 콘텐츠를 정의 되지 않은 상태일 수 있습니다.|  
|`PageRange`|XML 요소|페이지 범위를 나타냅니다.|  
|`PageRange/@Offset`|특성, 정수|Hello 오프셋 hello 전송 파일과 hello blob hello 페이지 범위를 지정 하는 위치에서 시작을 지정 합니다. 이 값은 512의 배수여야 합니다.|  
|`PageRange/@Length`|특성, 정수|Hello 페이지 범위의 hello 길이 지정합니다. 이 값은 512의 배수이고 4MB 이하여야 합니다.|  
|`PageRange/@Hash`|특성, 문자열|Hello 페이지 범위에 대 한 hello Base16 인코딩된 MD5 해시 값을 지정합니다.|  
|`BlockList`|중첩 XML 요소|블록의 이름을 지정한 블록 Blob에 필요합니다.<br /><br /> 가져오기 작업에 대 한 hello 블록 목록은 Azure 저장소로 가져올 블록의 집합을 지정 합니다. 내보내기 작업에 대 한 hello 블록 목록은 각 블록 hello hello 내보내기 디스크 파일에 저장 된 위치를 지정 합니다. 각 블록 hello 파일과 블록 길이가;에 있는 오프셋 하 여 설명 각 블록은 블록 ID 특성을 사용 하 여 추가로 이름이 지정 하며 hello 블록에 대 한 MD5 해시를 포함 합니다. Too50, 위로 000 블록 blob를 사용 하는 toodescribe 될 수 있습니다.  모든 블록 순서를 지정 해야 오프셋 및 함께 hello hello 파일의 전체 범위를 다루어야 *즉,*, 블록 사이 간격 없는 이어야 합니다. Hello blob 각 블록에 대해 개 이하의 64MB hello 블록 Id가 없는 모든 또는 모두 제공 합니다. 블록 Id는 필수 toobe Base64 인코딩 문자열입니다. 블록 ID에 대한 추가 요구 사항은 [블록 배치](/rest/api/storageservices/put-block)를 참조하세요.|  
|`Block`|XML 요소|블록을 나타냅니다.|  
|`Block/@Offset`|특성, 정수|Hello 오프셋 hello 지정 된 블록의 시작 위치를 지정 합니다.|  
|`Block/@Length`|특성, 정수|Hello 블록;에 hello 바이트 수를 지정합니다. 이 값은 최대 4MB 이어야 합니다.|  
|`Block/@Id`|특성, 문자열|Hello 블록에 대 한 hello 블록 ID를 나타내는 문자열을 지정 합니다.|  
|`Block/@Hash`|특성, 문자열|Hello 블록의 hello Base16 인코딩된 MD5 해시를 지정합니다.|  
|`Blob/MetadataPath`|문자열|선택 사항입니다. Hello 메타 데이터 파일의 상대 경로 지정합니다. 가져오기 작업 중 hello 메타 데이터는 hello 대상 blob에 설정 됩니다. 내보내기 작업 중 hello blob의 메타 데이터는 hello 드라이브에 hello 메타 데이터 파일에 저장 됩니다.|  
|`Blob/MetadataPath/@Hash`|특성, 문자열|Hello blob의 메타 데이터 파일의 hello Base16 인코딩된 MD5 해시를 지정합니다.|  
|`Blob/PropertiesPath`|문자열|선택 사항입니다. Hello 속성 파일의 상대 경로 지정합니다. 가져오기 작업 중 hello 속성 hello 대상 blob에 설정 됩니다. 내보내기 작업 중 hello blob 속성 hello 드라이브에 hello 속성 파일에 저장 됩니다.|  
|`Blob/PropertiesPath/@Hash`|특성, 문자열|Hello blob의 속성 파일의 hello Base16 인코딩된 MD5 해시를 지정합니다.|  
  
## <a name="next-steps"></a>다음 단계
 
* [저장소 Import/Export REST API](/rest/api/storageimportexport/)
