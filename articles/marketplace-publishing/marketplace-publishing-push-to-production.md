---
title: "aaaDeploy 프로그램 제안 toohello Azure 마켓플레이스 | Microsoft Docs"
description: "에 대해 알아보고 제안을-가상 컴퓨터 이미지, 개발자 서비스, 데이터 서비스 등-Azure 마켓플레이스 toohello hello 지침 toodeploy 과정을 안내 합니다."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 8f79b891-84e2-4f41-ba0d-66420e2c6b2e
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2016
ms.author: hascipio
ms.openlocfilehash: ab0bb7c78020187505c2d5f09c4de246987ecd97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-offer-toohello-azure-marketplace"></a>사용자 제공 toohello Azure 마켓플레이스에서 배포
모두 만족 제안 된 (즉, 테스트 한 고객 시나리오, 콘텐츠, 등 마케팅) 준비 toolaunch 되며 요청 **tooproduction 푸시** hello에 **게시** 탭 합니다.  

1. hello 연습 페이지에서 hello 4 단계에서 hello 포털을 게시 해야 완료 된 작업과 녹색입니다. 가상 컴퓨터 서비스에 대 한 지침을 따르면 해당 hello 처리 되는지 확인 합니다.
   
    ![drawing][img-pubportal-walkthru-checked]
2. 선택 hello **게시** hello hello 왼쪽 목록에서 탭 합니다.
   
    ![drawing][img-pubportal-menu-publish]
3. Hello 단추 클릭 **요청 승인 toopush tooproduction**합니다. Hello 요청이 면 hello 승인 팀 최종 검토를 실행 하 고 제안을 hello Azure Marketplace에서에서 사용할 수 있습니다.
   
    ![drawing][img-pubportal-publish-pushproduction]

> [!IMPORTANT]
> 가상 컴퓨터의 경우 hello 단추 요청 승인 toopush tooproduction 클릭 하면 다음 단계는 hello hello 장면 뒤 수행 됩니다. Hello hello 게시 탭에서 각 단계의 수 tooview hello 진행 됩니다. 포털을 게시 합니다. 확인 해야이 페이지 일정 한 간격 (표시 될 때까지 hello 상태 "표시")에서 최종 수정 해야 하는 모든 오류 정보.
> 
> * 처음에 프로덕션 요청 toohello 인증 팀 hello vhd의 유효성을 검사 하 게 이동 합니다. 그러나 이미 나열 된 자신의 구독을 업데이트 하는 경우 변경만 마케팅 hello 요청 하기 전 다음 hello 인증 단계를 건너뜁니다.
> * Hello 다음 단계에서 hello 요청 hello 제공의 콘텐츠를 마케팅 hello 확인 toohello 콘텐츠 유효성 검사 팀을 제공 됩니다.
> * 단계는 hello 성공 하면 프로덕션 환경에서 hello 제공 승인 됩니다. 이때 hello 상태 될 "에 나열 된" hello 게시 포털입니다. 그러나이 "나열" 상태는 hello 프로세스가 완료 된을 의미 하지 않습니다. 다음 단계가 필요 toobe hello 제공 하기 전에 완료 hello hello Azure Marketplace에서에서 제공 됩니다.
> * Hello 제공 위의 hello 단계에서 프로덕션 환경에서 승인 되 면 모든 hello 제공 시작의 복제 hello Azure 데이터 센터입니다. 일반적으로 복제 toocomplete hello에 대 한 24 48hours 걸리지만 hello vhd의 hello 크기에 따라 tooa 주를 차지할 수 있습니다. 그러나 이미 나열 된 자신의 구독을 업데이트 하는 경우 변경만 마케팅 하기 전 다음 hello 복제가 빠릅니다.
> * Hello 복제가 완료 되 면 hello 제공 hello Azure Marketplace에서에서 사용할 수 됩니다.
> 
> 삭제할 수 있습니다 hello 제공 되는 동안는 **초안** 상태 (즉, 되지 **toostaging 푸시** 또는 **tooproduction 푸시**). Hello에 **기록** 탭에서 hello **초안을 삭제** hello 페이지 toodelete hello 맨 아래에 초안 단추입니다.
> 
> 

## <a name="production-checklist-for-all-virtual-machine-offers"></a>모든 가상 컴퓨터 제품에 대한 프로덕션 검사 목록
* Microsoft Azure Certified 파트너인지 확인합니다.
* Hello Sku 탭 아래에서 hello 옵션 "숨기면이 SKU hello Marketplace에서에서 솔루션 템플릿을 통해 항상 구입 해야 하기 때문 에" 됨으로 표시 되어야 합니다만 예 hello SKU 솔루션 템플릿을의 일부인 경우. 모든 다른 경우 hello,이 옵션으로 아니요. 항상 표시 되어야 합니다.
* 기억: 바꾸지 않아야 hello SKU 표시 유형 설정이 hello SKU가 나열 되 면 합니다. 이 기능은 지원되지 않습니다.
* Hello 로고 toohello Azure 마켓플레이스 로고 지침 아래에 지정 된 준수를 확인 합니다.
* 제품 및 SKU 설명은 달라야 합니다.
* SKU의 제목 및 제품의 자세한 설명은 달라야 합니다.
* SKU 제목 및 제품 요약은 달라야 합니다.
* 여러 SKU가 있는 제품에서 SKU 제목을 서로 달라야 합니다.

**Azure 마켓플레이스 로고 지침**

* hello Azure 디자인 간단한 색상표를 있습니다. Hello 수가 기본과 보조 색 로고에 낮게 유지 합니다.
* hello Azure 포털의 hello 테마 색 흰색은 검정입니다. 따라서 hello 프로그램 로고의 배경색으로 이러한 색을 사용 하지 마십시오. 로고 프로그램 hello Azure 포털에서에서 관련성이 하 게 만드는 몇 가지 색을 사용 합니다. 간단한 기본 색을 사용하는 것이 좋습니다. 투명 한 배경을 사용 하는 경우 해당 hello 로고/텍스트가 검정색 또는 흰색 아닌지 확인 합니다.
* 그라데이션 배경이 hello 로고에 사용 하지 마십시오.
* 텍스트, 회사 또는 브랜드 이름으로도 hello 로고에 배치 하지 마십시오.
* 로고의 hello 모양과 느낌 '플랫' 해야 하며 그라데이션 하지 않아야 합니다.
* hello 로고 늘이는 없습니다.

**Hello Hero 로고에 대 한 추가 지침:**

* hello Hero 로고 선택 사항입니다. hello 게시자 하지 tooupload Hero 로고를 선택할 수 있습니다. **그러나 한 번 업로드 된 hello hero 아이콘 hello에서 삭제할 수 없습니다 포털을 게시 합니다. 그 당시 hello 파트너 지침을 따라야 hello Azure 마켓플레이스 Hero 아이콘에 대 한 다른 hello 제안을 승인 된 tooproduction 되지 것입니다.**
* 게시자 표시 이름, SKU 제목과 hello hello 긴 요약 흰색 글꼴 색에 표시 되 제공 합니다. 따라서 hello Hero 아이콘의 hello 백그라운드로 밝은 색을 유지 하지 마십시오. 대표 아이콘에는 검은색, 흰색 및 투명한 배경이 허용되지 않습니다.
* hello 게시자 표시 이름, SKU 제목, 긴 요약 hello 제안 및 hello 만들기 단추 hello 제안을 나열 되 면 hello Hero 로고 내부 프로그래밍 방식으로 포함 됩니다. 따라서 hello Hero 로고를 디자인 하는 텍스트를 입력 해야 합니다. (즉, 게시자 표시 이름, SKU 제목, 긴 요약 hello 제공) hello 텍스트 포함 되므로 프로그래밍 방식으로 자체 저기 hello 오른쪽에 빈 공간을 둡니다. hello 텍스트에 대 한 hello 빈 공간 415 x 100 hello 오른쪽에 있어야 합니다. (및 것은 370px hello 왼쪽에서 오프셋).

## <a name="additional-production-checklist-for-already-listed-virtual-machine-offers"></a>이미 나열된 가상 컴퓨터 제품에 대한 추가 프로덕션 검사 목록
* 회사에서 이름을 이미 있는 경우 hello로 제공 하는 서비스 제공 동일 확인 하십시오. 그렇다면 새 중복 제안을 만드는 대신 기존 제공 hello에에서 새 버전의 hello SKU 추가 해야 합니다.
* 데이터 디스크 변경 안 hello의 두 버전 간에 동일한 SKU입니다.
* hello Azure 마켓플레이스 지원 하지 않습니다 가격이 변경 hello의 SKU는 항목으로 목록 hello 기존 고객의 hello 청구에 영향을 줍니다. Hello SKU를 사용할 수 있는 hello 영역에 나열 된 hello Sku의 가격 책정 hello를 변경 하지 않는 것을 확인 합니다. 그러나 있습니다 수 새 Sku 추가 하거나 기존 SKU 새 영역 tooan 합니다.

## <a name="next-steps"></a>다음 단계
Hello 제공 가동 되기, 테스트 모든 hello 계약 및 기능이 작동 하는 hello 고객 시나리오 toovalidate 제대로 hello 프로덕션 환경에서 테스트 된 및의 유효성이 검사 된 hello 스테이징 환경으로.

## <a name="see-also"></a>참고 항목
* [시작 하기: 어떻게 toopublish 제안 toohello Azure 마켓플레이스](marketplace-publishing-getting-started.md)

[img-pubportal-walkthru-checked]:media/marketplace-publishing-push-to-production/pubportal-walkthru-checked.png
[img-pubportal-menu-publish]:media/marketplace-publishing-push-to-production/pubportal-menu-publish.png
[img-pubportal-publish-pushproduction]:media/marketplace-publishing-push-to-production/pubportal-publish-pushproduction.png
