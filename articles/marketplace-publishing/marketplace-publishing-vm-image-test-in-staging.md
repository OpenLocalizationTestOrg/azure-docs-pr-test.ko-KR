---
title: "마켓플레이스 hello에 대 한 VM 제공 aaaTest | Microsoft Docs"
description: "어떻게 tootest VM의 이미지 hello Azure 마켓플레이스를 이해 합니다."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 7a41c3c6-625c-4478-b804-e124dee89040
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: hascipio
ms.openlocfilehash: ab166d2c3c536810a3a8f48330f0482b9b4e58d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="test-your-vm-offer-for-hello-azure-marketplace-in-staging"></a>준비 단계에서 Azure 마켓플레이스 hello에 대 한 VM 제안을 테스트합니다
테스트 하 고 toohello 마켓플레이스를 배포 하기 전에 해당 기능을 확인 수 "샌드박스" 전용 사용자 SKU를 배포 하는 수단을 준비 합니다. hello SKU가 배포 tooa 고객과 마찬가지로 준비에 나타납니다. VM 이미지에는 인증 된 toobe 푸시 toostaging 이어야 합니다.

## <a name="step-1-push-your-offer-toostaging"></a>1 단계: 제안 toostaging 푸시
1. Hello에 **게시** 탭을 클릭 **tooStaging 푸시**합니다.
   
    ![drawing](media/marketplace-publishing-vm-image-test-in-staging/vm-image-push-to-staging.png)
2. 게시 포털 hello 오류가 발생 하는 메시지를 표시를 수정 합니다.
3. Hello에 **준비 된 제안을 액세스할 수 있는 사용자?** 대화 상자를 사용 하 여 toopreview 제안을 hello에 Azure 구독 hello 목록을 입력 [Azure preview 포털](https://portal.azure.com)합니다.
   
   > [!NOTE]
   > 가상 컴퓨터 및 솔루션 템플릿의 경우 CSP, DreamSpark 또는 Azure in Open 형식의 구독을 허용 목록에 **추가하지 마세요** .
   > 
   > 

    > Hello 단추를 클릭할 때 가상 컴퓨터의 경우 **푸시 tooSTAGING**, 단계를 수행 하는 hello hello 장면 뒤 수행 됩니다. Hello hello 게시 탭에서 각 단계의 수 tooview hello 진행 됩니다. 포털을 게시 합니다. 확인 해야이 페이지 일정 한 간격 (될 때까지 준비 된 hello 상태에 표시 됨)에서 최종 수정 해야 하는 모든 오류 정보.

    > - 준비 요청은 처음에 hello vhd의 유효성을 검사 하는 toohello 인증 팀을 설명 합니다. 그러나 요청이 변경만 마케팅 하기 전, 후 hello 인증 단계를 건너뜁니다.
    > - Hello 인증 완료 되 면 모든 hello 제공 시작의 복제 hello Azure 데이터 센터입니다. 일반적으로 복제 toocomplete hello에 대 한 24 48hours 걸리지만 hello vhd의 hello 크기에 따라 tooa 주를 차지할 수 있습니다. 그러나 요청이 변경만 마케팅 전 하는 경우 다음 hello 복제가 빠릅니다.
    > - Hello 복제가 완료 되 면 다음 hello 제안을 사용할 수 있습니다 hello에 [Azure 포털](http:/portal.azure.com)합니다. Hello에 준비 될 상태에서 해당 시간 hello 포털을 게시 합니다. 준비 된 서비스는 hello에 표시 [Azure 포털](http:/portal.azure.com) hello 전자 메일 id(s)는 hello로 행사를 준비 하는 hello 구독과 관련 된 사용 해야만 합니다.

1. Toohello 로그인 [Azure preview 포털](https://portal.azure.com) hello 중 하나를 사용 하 여 hello 이전 단계에서 나열 된 Azure 구독.
2. 제품을 찾고 VM 이미지 지점의 유효성을 검사합니다.
   
   * 콘텐츠를 마케팅에 표시 되는지 올바르게 hello 마켓플레이스 있는지 확인 합니다.
   * Hello VM 이미지의 종단 간 배포 합니다.
     
      ![img-map-portal](media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg)

> [!IMPORTANT]
> Hello 게시 포털을 통해 Microsoft에 알린다는 될 때까지 준비에 제안을 남습니다 [**게시** 탭 > hello 단추를 클릭 **"요청 승인 tooPush tooProduction"**] 준비 toopush는 tooproduction 합니다. 이 팀의 모든 멤버를 이동 나열 된 자신의 구독에는 준비 과정에서의 모든 것이 확인 하는 이상적인 시간 toohave입니다.
> 
> 플랫폼을 준비 하는 hello hello 게시자가 미리 보기 모드에서 테스트 hello 제공 하도록 설계 되었습니다. 이 플랫폼은 상용으로는 사용하지 않는 것이 좋습니다.
> 
> 

## <a name="next-steps"></a>다음 단계
제안을 "준비" 하 고 테스트의 기능 및 콘텐츠를 마케팅, 했으므로 toohello 최종 게시를 진행할 수 있습니다 단계 **4 단계**: [배포 하 여 제안을 toohello 마켓플레이스](marketplace-publishing-push-to-production.md)합니다.

## <a name="see-also"></a>참고 항목
* [시작 하기: 어떻게 toopublish 제안 toohello Azure 마켓플레이스](marketplace-publishing-getting-started.md)

