---
title: "데이터 서비스 마켓플레이스 hello에 대 한 제공 aaaTesting | Microsoft Docs"
description: "이해 어떻게 tootest 데이터 서비스는 hello Azure Marketplace에 대 한을 제공 합니다."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e861bd11-f74d-4d77-b4b5-23fb463644ad
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 1b9c7027d8e0818b9bdee5cfca971bab25dd1959
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="testing-your-data-service-offer-in-staging"></a>스테이징에서 데이터 서비스 제품 테스트
> [!IMPORTANT]
> **현재는 새 데이터 서비스 게시자 등록을 더 이상 받지 않고 있습니다. 따라서 새 데이터 서비스 등재 승인을 받을 수 없습니다.** SaaS 비즈니스 응용 프로그램의 경우 원하는 toopublish AppSource에 자세한 정보를 찾을 수 [여기](https://appsource.microsoft.com/partners)합니다. IaaS 응용 프로그램 또는 서비스 개발자 경우는 Azure 마켓플레이스에서 toopublish 같은 자세한 정보를 찾을 수 [여기](https://azure.microsoft.com/marketplace/programs/certified/)합니다.
> 
> 

Hello의 처음 두 단계를 완료 한 후 [Microsoft 개발자 계정 만들기](marketplace-publishing-accounts-creation-registration.md) 및 [게시 포털에서 데이터 서비스 제공을 만드는](marketplace-publishing-data-service-creation.md) hello에서 제안을 사용 가능 준비가 되었습니다. Azure 마켓플레이스에 적용 됩니다. 이 항목은 과정을 단계별로 hello 먼저, 중간, 호출된 "준비" 단계

개인 테스트 하 고 tooproduction 푸시하기 전에 해당 기능을 확인 수 "샌드박스"에 있는 제품을 배포 하는 수단을 준비 합니다. hello 제공이 배포 tooa 고객과 마찬가지로 준비에 표시 됩니다.

## <a name="step-1-pushing-your-offer-toostaging"></a>1단계. 제안 toostaging 푸시
제안 toostaging 푸시하여 있습니다 tootest hello 제안을 사용할 수 있는 toofuture 구독자 되기 전에.  제안을 표시 되 고 tooyour 데이터를 구독 하는 것에 대 한 작동 방식을 확인할 수 있습니다.  

  ![drawing](media/marketplace-publishing-data-service-test-in-staging/step-1.1.png)

1. Hello에 로그인 [게시 포털](https://publish.windowsazure.com)
2. 선택 **데이터 서비스** hello 왼쪽된 탐색 창에서
3. Toopush toostaging 원하는 제안을 선택 합니다. Hello 화면 위에 표시 됩니다.
4. 클릭 **tooStaging 푸시** 단추입니다.  
5. 문제가 있는 경우 hello로 toobe 필요한 제안을 완료 이전 toopushing toostaging, 표시 된 목록에 표시 됩니다.  Hello 목록의 각 항목을 클릭 하 여 이러한 항목을 수정 합니다. 모든 수정 사항은를 클릭 하면 **tooStaging 푸시** 단추를 다시 합니다.

제안 된 문제가 없는지 아래 hello 팝업 창이 표시 됩니다.  

모르는 경우 계획/not 승인 toosurface Azure 포털에 있는 제품 (현재을 제한 한 용량) 한 다음 방금 닫기 hello 팝업 창.

tootest (더하기 toohello DataMarket 포털)에서 Azure 포털에서 데이터 서비스를 사용 하는 Azure 구독 ID tootest이 필요 합니다.  이 구독 ID는 hello 계정 명시 됩니다 tootest 제안을 허용 합니다.  

잘라내기 구독 ID를 붙여 넣고 hello 확인 표시 toocontinue를 클릭 합니다.

  ![drawing](media/marketplace-publishing-data-service-test-in-staging/step-1.2.png)

> [!NOTE]
> Azure 구독 Id는만 테스트 하 고 hello를 준비 하는 데 필요한 [Azure 관리 포털](https://manage.windowsazure.com)합니다. Azure Marketplace에서 필요한 tootest 하지 않습니다.
> 
> 

hello 다음 화면에 나타나는 표시는 게시 수행 되 고 "진행 중" 에"hello를 표시 하 여 아이콘 아래 노란색으로 강조 표시 합니다. 10 too15 분 걸리며 toostaging 푸시합니다.  이보다 오래 걸리면 우선 브라우저를 새로 고칩니다.  Hello 드문 경우 지만 자신의 구독 한 시간 후 toostaging 푸시할 여전히는 us 연결 문제가 있다는 것을 알려주세요 toolet hello 연락처를 클릭 합니다.

  ![drawing](media/marketplace-publishing-data-service-test-in-staging/step-1.3.png)

Hello 푸시 tooStaging hello 완료 되 면 "에서"진행 중 아이콘 이동 중지 되 고 너무 "준비" hello 상태가 업데이트 됩니다.  사용자는 이제 준비 tootest 제안 합니다.  

## <a name="step-2-test-your-staged-offer-in-datamarket"></a>2단계. DataMarket에서 준비된 제품 테스트
Hello 텍스트 다음 hello 링크를 클릭 **"에서 제공 하 여 서비스를 참조 하십시오. …"** 구독자 hello toodisplay hello 화면 제안을 tooproduction 될 때 표시 되 고 DataMarket에 표시 됩니다.

  ![drawing](media/marketplace-publishing-data-service-test-in-staging/step-2.2.png)

모든 로고, 가격/트랜잭션, 텍스트, 이미지, 설명서, tooensure 위에 표시 된 각 hello 12 항목 제대로 링크는 작업 하 고 올바른지 확인 하거나 테스트 합니다.  이 실제 값으로 대체 되었습니다 제안을 만들 때 입력 한 모든 테스트 값 좋은 시간 tooensure입니다.

1. 제품 로고
2. Offer name
3. 게시자 이름/링크 tooyour 회사 웹 사이트
4. 제품에 대한 검색 범주
5. 제품의 지원 링크 tooassist 구독자
6. 제품에 대한 상황별 설명
7. 청구 세부 정보를 설명하는 제품 계획
8. 링크 tooimplementation 코드
9. 제품 데이터 사용을 보여주는 샘플 이미지
10. Hello 제공 내에서 각 서비스에 대 한 입/출력 메타 데이터
11. 제품 사용 약관
12. Hello 제품 데이터의 미리 보기

마지막으로 검사 hello 서비스는 hello 링크 "이 데이터 집합 탐색" 클릭 하 여 hello Datamarket 통해 작동 합니다.  새 창이 열립니다 hello 도구에서 이라고 "서비스 탐색기" 서비스에 대해 hello 쿼리 결과 미리 볼 수 있도록 합니다.  이 창에서 매개 변수는 필요 하 고 서비스에 대 한 쿼리에서 표시 hello 결과 확인 하는 hello를 입력할 수 있습니다.   또한 표시 된 쿼리에 대 한 hello URL입니다.  

> [!NOTE]
> 수 있는지 tooreview hello 텍스트 hello 서비스 설명 hello 위쪽에 표시 됩니다.  제안을 하나 이상의 서비스로 구성 된 호출 hello 아래쪽 tooswitch toohello 다음 서비스 tooreview에 hello 탭 클릭 및 테스트 합니다.
> 
> 

## <a name="next-step"></a>다음 단계
문제가 있고 해결하기 위해서 도움이 필요하면 [Azure Publisher Support](http://go.microsoft.com/fwlink/?LinkId=272975)에 문의하세요.

만족 스 러 우면 및 준비 toopublish 읽기 hello 하십시오 제안을 [요청 승인 tooPush tooProduction](marketplace-publishing-push-to-production.md) 설명서입니다.

## <a name="see-also"></a>참고 항목
* [시작 하기: 어떻게 toopublish 제안 toohello Azure 마켓플레이스](marketplace-publishing-getting-started.md)

