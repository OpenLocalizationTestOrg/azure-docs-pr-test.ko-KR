---
title: "XML 유효성 검사-Azure 논리 앱에 대 한 aaaSchemas | Microsoft Docs"
description: "Azure Logic Apps 및 엔터프라이즈 통합 팩용 스키마로 XML 문서 유효성 검사"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 56c5846c-5d8c-4ad4-9652-60b07aa8fc3b
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 87cf92741e10ff7cccd260f27442909e34928903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-with-schemas-for-azure-logic-apps-and-hello-enterprise-integration-pack"></a>Azure 논리 앱 및 엔터프라이즈 통합 팩 hello에 대 한 XML 스키마 유효성 검사

스키마 확인 하 고 나타나면 hello XML 문서가 모두 유효한 hello 예상한 데이터를 미리 정의 된 형식에서입니다. 스키마는 B2B 시나리오에서 교환되는 메시지의 유효성을 검사하는 데 도움이 됩니다.

## <a name="add-a-schema"></a>스키마 추가

1. Hello Azure 포털에서에서 선택 **더 많은 서비스**합니다.

    ![Azure Portal, "더 많은 서비스"](media/logic-apps-enterprise-integration-schemas/overview-11.png)

2. Hello 필터 검색 상자에 입력 **통합**를 선택 하 고 **통합 계정** hello 결과 목록에서 합니다.

    ![필터 검색 상자](media/logic-apps-enterprise-integration-schemas/overview-21.png)

3. 선택 hello **통합 계정** tooadd hello 스키마 원하는 합니다.

    ![통합 계정 목록](media/logic-apps-enterprise-integration-schemas/overview-31.png)

4. Hello 선택 **스키마** 바둑판식으로 배열입니다.

    ![예제 통합 계정, "스키마"](media/logic-apps-enterprise-integration-schemas/schema-11.png)

### <a name="add-a-schema-file-smaller-than-2-mb"></a>2MB보다 작은 스키마 파일 추가

1. Hello에 **스키마** hello 이전 단계), (에서 열리면 선택 블레이드 **추가**합니다.

    ![스키마 블레이드, "추가"](media/logic-apps-enterprise-integration-schemas/schema-21.png)

2. 스키마의 이름을 입력합니다. Hello 폴더 다음 toohello 아이콘을 선택 하 여 hello 스키마 파일을 업로드 **스키마** 상자입니다. Hello 업로드 프로세스가 완료 된 후 선택 **확인**합니다.

    !["작은 파일"이 강조 표시된 "스키마 추가" 스크린샷](media/logic-apps-enterprise-integration-schemas/schema-31.png)

### <a name="add-a-schema-file-larger-than-2-mb-up-too8-mb-maximum"></a>스키마 파일 (위쪽 too8 MB 최대) 2MB 이상의 추가

이러한 단계 hello blob 컨테이너 액세스 수준에 따라 다릅니다: **공용** 또는 **익명 액세스할 수 없는**합니다.

**toodetermine이 액세스 수준**

1.  **Azure Storage 탐색기**를 엽니다. 

2.  아래 **Blob 컨테이너**선택, 원하는 hello blob 컨테이너입니다. 

3.  **보안**, **액세스 수준**을 선택합니다.

Hello blob 보안 액세스 수준이 **공용**, 다음이 단계를 수행 합니다.

!["Blob 컨테이너", "보안" 및 "공용"이 강조 표시된 Azure Storage 탐색기](media/logic-apps-enterprise-integration-schemas/blob-public.png)

1. Hello 스키마 tooyour 저장소 계정에 업로드 하 고 hello URI를 복사 합니다.

    ![URI가 강조 표시된 저장소 계정](media/logic-apps-enterprise-integration-schemas/schema-blob.png)

2. **스키마 추가**선택, **큰 파일**, hello에 hello URI를 제공 하 고 **콘텐츠 URI** 입력란.

    !["추가" 단추 및 " 큰 파일"이 강조 표시된 스키마](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

Hello blob 보안 액세스 수준이 **익명 액세스할 수 없는**, 다음이 단계를 수행 합니다.

!["Blob 컨테이너", "보안" 및 "익명 액세스 없음"이 강조 표시된 Azure Storage 탐색기](media/logic-apps-enterprise-integration-schemas/blob-1.png)

1. Hello 스키마 tooyour 저장소 계정에 업로드 합니다.

    ![저장소 계정](media/logic-apps-enterprise-integration-schemas/blob-3.png)

2. Hello 스키마에 대 한 공유 액세스 서명을 생성 합니다.

    ![공유 액세스 서명 탭이 강조 표시된 저장소 계정](media/logic-apps-enterprise-integration-schemas/blob-2.png)

3. **스키마 추가**선택, **큰 파일**, hello에 hello 공유 액세스 서명 URI를 제공 하 고 **콘텐츠 URI** 텍스트 상자입니다.

    !["추가" 단추 및 " 큰 파일"이 강조 표시된 스키마](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

4. Hello에 **스키마** 통합 계정 블레이드를 새로 추가 된 스키마 표시 되어야 합니다.

    ![통합 계정에 "스키마" 및 강조 표시 하는 hello 새 스키마](media/logic-apps-enterprise-integration-schemas/schema-41.png)

## <a name="edit-schemas"></a>스키마 편집

1. Hello 선택 **스키마** 바둑판식으로 배열입니다.

2. Hello 후 **스키마** tooedit 선택 hello 스키마 블레이드에서 열립니다.

3. Hello에 **스키마** 블레이드에서 선택 **편집**합니다.

    ![스키마 블레이드](media/logic-apps-enterprise-integration-schemas/edit-12.png)

4. 선택 hello 스키마 파일을 tooedit, 원하는 선택한 다음 하면 **열려**합니다.

    ![파일 tooedit 스키마 열기](media/logic-apps-enterprise-integration-schemas/edit-31.png)

스키마 hello 메시지를 azure에서는 성공적으로 업로드 합니다.

## <a name="delete-schemas"></a>스키마 삭제

1. Hello 선택 **스키마** 바둑판식으로 배열입니다.

2. Hello 후 **스키마** toodelete 선택 hello 스키마 블레이드에서 열립니다.

3. Hello에 **스키마** 블레이드에서 선택 **삭제**합니다.

    ![스키마 블레이드](media/logic-apps-enterprise-integration-schemas/delete-12.png)

4. tooconfirm toodelete hello 않겠다고 선택한 스키마를 선택 **예**합니다.

    !["스키마 삭제" 확인 메시지](media/logic-apps-enterprise-integration-schemas/delete-21.png)

    Hello에 **스키마** 블레이드에서 hello 스키마 목록을 새로 고치고 더 이상 삭제 된 hello 스키마를 포함 합니다.

    !["스키마"가 강조 표시된 통합 계정](media/logic-apps-enterprise-integration-schemas/delete-31.png)

## <a name="next-steps"></a>다음 단계
* [엔터프라이즈 통합 팩 hello에 대 한 자세한](logic-apps-enterprise-integration-overview.md "hello 엔터프라이즈 통합 팩에 대 한 자세한 정보")합니다.  

