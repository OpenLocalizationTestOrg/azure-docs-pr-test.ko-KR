---
title: "aaaGuide toocreating hello 마켓플레이스를 위한 솔루션 템플릿 | Microsoft Docs"
description: "Toocreate, 인증 및 hello Azure Marketplace에서 구입에 대 한 다중 VM 이미지 솔루션 템플릿을 배포 방법을 설명 합니다."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e14e05f2-2385-4ce0-b351-0747cb74ba19
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: b0e7067176337dd0d3f6f6ec04c963f80f706ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toocreate-a-solution-template-for-azure-marketplace"></a>Azure 마켓플레이스 toocreate 솔루션 템플릿을 안내합니다
1 단계를 완료 한 후 [계정 만들기 및 등록][link-acct-creation], 우리 있습니다 hello 만들기에 Azure 호환 솔루션 서식 파일의 단계별 [을 만들기 위한 필수 구성 요소를 기술는 솔루션 템플릿을](marketplace-publishing-solution-template-creation-prerequisites.md)합니다. 이제 우리는 단계를 안내 hello 여러 Vm hello에 대 한 솔루션 템플릿을 만들기 위한 [게시 포털] [ link-pubportal] hello Azure Marketplace에 대 한 합니다.

## <a name="create-your-solution-template-offer-in-hello-publishing-portal"></a>Hello 게시 포털에에서 사용자 솔루션 템플릿을 제안을 만듭니다.
너무 이동 [https://publish.windowsazure.com](http://publish.windowsazure.com)합니다. 첫 번째 시간 toohello hello에 대 한 로그인 할 때 [게시 포털](https://publish.windowsazure.com/)를 사용 하 여 hello 회사의 판매자 프로필 등록 된 계정과 동일 합니다. 이상에서는 hello 게시 포털에서에서 공동 관리자로 모든 직원이 회사의를 추가할 수 있습니다.

### <a name="1-select-solution-templates"></a>1. "솔루션 템플릿" 선택
  ![drawing][img-pubportal-menu-sol-templ]

### <a name="2-create-a-new-solution-template"></a>2. 새 솔루션 템플릿 만들기
  ![drawing][img-pubportal-sol-templ-new]

### <a name="3-start-with-topologies"></a>3. 토폴로지로 시작
솔루션 템플릿은 해당 토폴로지의 "부모" tooall입니다. 하나의 제품/솔루션 템플릿에서 여러 토폴로지를 정의할 수 있습니다. 제안을 toostaging 푸시를 모든 해당 토폴로지에 하 여 전달 합니다. 제안을 toodefine 아래 hello 단계를 수행 합니다.     

* 토폴로지 생성: 일반적으로 "토폴로지 식별자" hello 솔루션 템플릿에 대 한 hello 토폴로지의 hello 이름입니다. 아래와 같이 hello 토폴로지 식별자 hello URL에 사용 됩니다.

  Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}

  Azure Portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}
* 새 버전을 추가합니다.

### <a name="4-get-your-topology-versions-certified"></a>4. 토폴로지 버전 인증받기
모든 필수 파일 tooprovision hello 토폴로지의 특정 버전을 포함 하는 zip 파일을 업로드 합니다. 이 zip 파일 hello 다음을 포함 해야 합니다.

* 루트 디렉터리의 *mainTemplate.json* 및 *createUiDefinition.json* 파일
* 연결된 모든 템플릿 및 모든 필수 스크립트

  > [!TIP]
  > 프로그램 개발자가 hello 솔루션 템플릿을 토폴로지를 만들고 얻거나 인증 hello 비즈니스에 작업 하는 동안, 마케팅 및/또는 법률 부서에 hello 마케팅 및 법적 콘텐츠 작업할 수 있습니다.
  >
  >

## <a name="next-steps"></a>다음 단계
솔루션 템플릿을 생성 하 고 hello zip 파일을 업로드 하세요 hello 지침에에서 따라 hello [마켓플레이스 마케팅 콘텐츠 가이드](marketplace-publishing-push-to-staging.md) hello 제공 toostaging 푸시하기 전에 합니다. toosee hello 전체 집합 문서를 게시 하는 marketplace의 참조 [시작: 어떻게 제공 toohello Azure 마켓플레이스 toopublish](marketplace-publishing-getting-started.md)합니다.

다음 관련 문서를 참조할 수도 있습니다.

* VM 이미지: [Azure의 가상 컴퓨터 이미지 정보](https://msdn.microsoft.com/library/azure/dn790290.aspx)
* VM 확장: [VM 에이전트 및 VM 확장 개요](https://msdn.microsoft.com/library/azure/dn832621.aspx) 및 [Azure VM 확장 및 기능](https://msdn.microsoft.com/library/azure/dn606311.aspx)
* Azure Resource Manager: [Azure Resource Manager 템플릿 작성](../azure-resource-manager/resource-group-authoring-templates.md) 및 [간단한 템플릿 예제](https://github.com/rjmax/ArmExamples)
* 저장소 계정 제한: [어떻게 저장소 계정 제한에 대 한 tooMonitor](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) 및 [프리미엄 저장소](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)

[img-pubportal-menu-sol-templ]:media/marketplace-publishing-solution-template-creation/pubportal-menu-solution-templates.png
[img-pubportal-sol-templ-new]:media/marketplace-publishing-solution-template-creation/pubportal-solution-template-new.png
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-pubportal]:https://publish.windowsazure.com
