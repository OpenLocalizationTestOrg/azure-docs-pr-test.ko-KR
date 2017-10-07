---
title: "Azure 검색 tooBlob aaaAdding 저장소 | Microsoft Docs"
description: "Hello Azure 검색 HTTP REST API를 사용 하 여 코드에서 인덱스를 만듭니다."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
ms.service: search
ms.topic: article
ms.date: 05/04/2017
ms.author: ashmaka
ms.openlocfilehash: a3801790067bf169693b500e83799286b7387a77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="searching-blob-storage-with-azure-search"></a>Azure Search로 Blob Storage 검색

Hello 다양 한 Azure Blob 저장소에 저장 된 콘텐츠 형식 내에서 검색 어려운 문제 toosolve 될 수 있습니다. 인덱스를 검색 하는 반면 Azure 검색을 사용 하 여 몇 번의 클릭에서 Blob의 내용을 hello 합니다. Blob Storage를 통해 검색하려면 Azure Search 서비스를 프로비전해야 합니다. Azure 검색의 가격대 hello에서 확인할 수 있습니다 및 다양 한 서비스 제한 hello [가격 책정 페이지](https://aka.ms/azspricing)합니다.

## <a name="what-is-azure-search"></a>Azure 검색이란?
[Azure 검색](https://aka.ms/whatisazsearch) 활용할 수 있는 tooweb 및 모바일 응용 프로그램에서 발생 하는 개발자가 tooadd 강력한 전체 텍스트 검색에 대 한 검색 솔루션입니다. 서비스와 Azure 검색 제거 hello 필요 toomanage 제공 하는 동안 모든 검색 인프라는 [99.9% 작동 시간 SLA](https://aka.ms/azuresearchsla)합니다.

Azure Search는 56개 언어의 고급 지원을 통해 사용자의 콘텐츠를 분석하고 언어별 구조를 지능적으로 처리할 수 있습니다. Azure 검색은 또한 hello 도구 toobuild 풍부한 검색 사용자 환경을 제공합니다. 패싯 탐색, typeahead 검색 제안 Azure 검색을 사용 하 여 적중 횟수 강조 toouser 인터페이스와 같은 간단한 tooadd 기능 것 합니다. Azure 검색의 기능에 대 한 toolearn, hello 서비스를 읽을 수 있습니다 [설명서](https://aka.ms/azsearchdocs)합니다.

## <a name="crack-open-and-search-through-hello-content-of-enterprise-document-formats"></a>Crack 열기 및 엔터프라이즈 문서 형식의 hello 콘텐츠를 검색
지 원하는 [추출 문서](https://aka.ms/azsblobindexer) Azure Blob 저장소에 Azure 검색의 다양 한 blob에 저장 된 파일 형식 hello 콘텐츠를 인덱싱할 수 있습니다.
- PDF
- Microsoft Office: DOCX/DOC, XLSX/XLS, PPTX/PPT, MSG(Outlook 메일)
- HTML
- 일반 텍스트 파일

텍스트 및 이러한 파일 형식의 메타 데이터를 추출 하 여 쉽게 toosearch는 것에서 여러 파일 형식 유형에 관계 없이 단일 쿼리 toofind hello 가장 관련성이 높은 문서에 사용 합니다. Blob 저장소 및 Azure 검색을 사용 하는 강력한 엔터프라이즈 콘텐츠 관리 솔루션의 Microsoft Office 문서, Pdf, 및 전자 메일, 가능한 toobuild hello 콘텐츠와 hello 메타 데이터를 인덱싱하고 있습니다.

## <a name="search-through-your-blob-metadata"></a>Blob 메타데이터에서 검색
모든 콘텐츠 형식의 blob 통해 쉽게 toosort 수행 하는 일반적인 시나리오는 hello 뿐만 아니라 tooindex hello에 대 한 사용자 지정, 사용자 정의 blob 메타 데이터 시스템 속성 각 blob에 대 한 합니다. 이러한 방식으로 각 blob에 대 한 정보는 모든 Blob 저장소 콘텐츠 hello 쉽게 정렬할 수 있도록 hello blob와 패싯 문서 종류에 관계 없이 인덱싱됩니다.

[Blob 메타데이터 인덱싱에 관해 자세히 알아보세요.](https://aka.ms/azsblobmetadataindexing)

## <a name="image-search"></a>이미지 검색
Azure 검색의 전체 텍스트 검색, 패싯 탐색 및 정렬 기능 적용된 toohello 메타 데이터의 blob에 저장 된 이미지 될 수 있습니다.

이러한 이미지가 미리 hello를 사용 하 여 처리 하는 경우 [컴퓨터 비전 API](https://www.microsoft.com/cognitive-services/computer-vision-api) Microsoft Cognitive 서비스에서 않으면 가능한 tooindex hello 시각적 콘텐츠 OCR 및 필기 인식을 포함 하 여 각 이미지에서 찾을 수 있습니다. OCR 오류 코드 및 기타 이미지 처리 기능 tooAzure 검색, 이러한 기능에 관심이 있는 경우 요청을 제출 하세요에 직접 추가 노력 하 고 우리의 [UserVoice](https://aka.ms/azsuv) 또는 [전자 메일을 보내](mailto:azscustquestions@microsoft.com)합니다.

## <a name="index-and-search-through-json-blobs"></a>JSON Blob을 통해 인덱스 만들기 및 검색
Azure 검색 JSON이 포함 된 blob에 구성 된 tooextract 구조적 콘텐츠를 수 있습니다. Azure 검색 JSON blob를 확인할 수 있으며 Azure 검색 문서 hello 적절 한 필드로 hello 구조적 콘텐츠를 구문 분석 됩니다. Azure 검색에는 각 요소 tooa 별도 Azure 검색 문서 매핑 및 JSON 개체의 배열을 포함 하는 blob도 사용할 수 있습니다.

Note JSON을 구문 분석 아닌지 현재 hello 포털을 통해 구성 가능 합니다. [Azure Search에서 JSON 구문 분석에 대해 자세히 알아보세요.](https://aka.ms/azsjsonblobindexing)

## <a name="quick-start"></a>빠른 시작
Azure 검색 hello Blob 저장소에 대 한 포털 블레이드에서 직접 tooblobs를 추가할 수 있습니다.

![](./media/search-blob-storage-integration/blob-blade.png)

Hello "추가 Azure 검색" 옵션을 클릭 하면 기존 Azure 검색 서비스를 선택 하거나 새 서비스를 만들 수 있는 흐름을 시작 합니다. 새 서비스를 만드는 경우 저장소 계정의 포털 환경 외부로 이동하게 됩니다. Toore 해야-toohello 저장소 포털 블레이드를 탐색 하 고 다시 hello 기존 서비스를 선택할 수 있는 hello "추가 Azure 검색" 옵션을 선택 합니다.

### <a name="next-steps"></a>다음 단계
전체 hello에 Azure 검색 Blob 인덱서 hello에 대 한 자세한 [설명서](https://aka.ms/azsblobindexer)합니다.
