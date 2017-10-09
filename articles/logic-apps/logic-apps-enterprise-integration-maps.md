---
title: "Azure 논리 앱-XSLT 맵이 포함 된 XML aaaTransform | Microsoft Docs"
description: "XSLT 맵 Azure 논리 앱 및 엔터프라이즈 통합 팩 hello tootransform XML 데이터를 추가 합니다."
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 90f5cfc4-46b2-4ef7-8ac4-486bb0e3f289
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 720e6f988b8542136dfcc402c3c463fcfb2f23cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-maps-for-xml-data-transform"></a>XML 데이터 변환을 위한 맵 추가

엔터프라이즈 통합 사용 하 여 형식 간에 tootransform XML 데이터를 매핑합니다. 지도 다른 형식으로 변환 해야 하는 문서에서 hello 데이터를 정의 하는 XML 문서. 

## <a name="why-use-maps"></a>맵을 사용하는 이유

정기적으로 나타나는 B2B 주문 또는 송장 날짜에 대 한 hello YYYMMDD 형식을 사용 하는 고객 으로부터 가정 합니다. 그러나 조직에서 hello MMDDYYY 형식으로 날짜를 저장할 수 있습니다. 지도도 사용할 수 있습니다*변환* 고객 활동 데이터베이스의 hello 순서 또는 송장 세부 정보를 저장 하기 전에 hello MMDDYYY에 hello YYYMMDD 날짜 형식.

## <a name="how-do-i-create-a-map"></a>맵을 만드는 방법

Hello로 BizTalk 통합 프로젝트를 만들 수 [엔터프라이즈 통합 팩](logic-apps-enterprise-integration-overview.md "hello 엔터프라이즈 통합 팩에 대 한 자세한 정보") Visual Studio 2015에 대 한 합니다. 그런 후 두 개의 XML 스키마 파일 간에 항목을 시각적으로 매핑할 수 있는 통합 맵 파일을 만들 수 있습니다. 이 프로젝트를 빌드하면 XSLT 문서가 생성됩니다.

## <a name="how-do-i-add-a-map"></a>맵을 추가하는 방법

1. Hello Azure 포털에서에서 선택 **찾아보기**합니다.

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. Hello 필터 검색 상자에 입력 **통합**을 선택한 후 **통합 계정** hello 결과 목록에서 합니다.

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. Tooadd hello 맵을 저장할 hello 통합 계정을 선택 합니다.

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. 선택 hello **지도** 바둑판식으로 배열입니다.

    ![](./media/logic-apps-enterprise-integration-maps/map-1.png)

5. Hello 지도 블레이드를 연 후 선택 **추가**합니다.

    ![](./media/logic-apps-enterprise-integration-maps/map-2.png)  

6. 맵의 **이름**을 입력합니다. tooupload hello 맵 hello hello 오른쪽에 hello 폴더 아이콘을 선택, 파일 **지도** 입력란. Hello 업로드 프로세스가 완료 되 면 선택 **확인**합니다.

    ![](./media/logic-apps-enterprise-integration-maps/map-3.png)

7. Azure의 hello 맵 tooyour 통합 계정을 추가한 맵 파일에 추가 된 있는지 여부를 표시 하는 화면에 나타나는 메시지를 가져옵니다. 이 메시지를 얻은 후 선택 hello **지도** 타일 새로 hello를 볼 수 있도록 맵을 추가 합니다.

    ![](./media/logic-apps-enterprise-integration-maps/map-4.png)

## <a name="how-do-i-edit-a-map"></a>맵을 편집하는 방법

원하는 hello 변경 내용으로 새 맵 파일을 업로드 해야 합니다. 처음 편집할 hello 맵을 다운로드할 수 있습니다.

hello 기존 맵을 대체 하는 새 맵을 tooupload 다음이 단계를 수행 합니다.

1. Hello 선택 **지도** 바둑판식으로 배열입니다.

2. Hello 지도 블레이드를 연 후 tooedit hello 맵을 선택 합니다.

3. Hello에 **지도** 블레이드에서 선택 **업데이트**합니다.

    ![](./media/logic-apps-enterprise-integration-maps/edit-1.png)

4. Hello 파일 선택에서 원하는 tooupload을 다음 선택 있습니다 hello 맵 파일을 선택 **열려**합니다.

    ![](./media/logic-apps-enterprise-integration-maps/edit-2.png)

## <a name="how-toodelete-a-map"></a>어떻게 toodelete 지도?

1. Hello 선택 **지도** 바둑판식으로 배열입니다.

2. Hello 지도 블레이드를 연 후 toodelete hello 맵을 선택 합니다.

3. **삭제**를 선택합니다.

    ![](./media/logic-apps-enterprise-integration-maps/delete.png)

4. Toodelete hello 지도 있는지 확인 합니다.

    ![](./media/logic-apps-enterprise-integration-maps/delete-confirmation-1.png)

## <a name="next-steps"></a>다음 단계
* [엔터프라이즈 통합 팩 hello에 대 한 자세한](logic-apps-enterprise-integration-overview.md "엔터프라이즈 통합 팩에 대 한 자세한 정보")  
* [규약에 대해 자세히 알아보기](../logic-apps/logic-apps-enterprise-integration-agreements.md "엔터프라이즈 통합 규약에 대해 알아보기")  
* [변환에 대해 자세히 알아보기](logic-apps-enterprise-integration-transform.md "엔터프라이즈 통합 변환에 대해 알아보기")  

