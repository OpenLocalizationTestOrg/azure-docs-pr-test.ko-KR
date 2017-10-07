---
title: "클라우드 서비스 배포 문제를 aaaTroubleshoot | Microsoft Docs"
description: "몇 가지 일반적인 문제는 클라우드 서비스 tooAzure를 배포할 때 발생할 수 있습니다. 이 문서에서는 그 중 솔루션 toosome 합니다."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: a18ae415-0d1c-4bc4-ab6c-c1ddea02c870
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 15aea4f2b2913d95f3378b2e9762b232531f3c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-deployment-problems"></a>클라우드 서비스 배포 문제 해결
클라우드 서비스 응용 프로그램 패키지 tooAzure를 배포할 때 hello에서 hello 배포에 대 한 정보를 얻을 수 있습니다 **속성** hello Azure 포털의에서 창. Hello 세부 정보를 사용할 수 있습니다 hello 클라우드 서비스 문제를 해결 하는이 창 toohelp으로 및 새로운 지원 요청을 열 때이 정보 tooAzure 지원을 제공할 수 있습니다.

Hello를 찾을 수 있습니다 **속성** 다음과 같이 창:

* 에 hello Azure 포털 클라우드 서비스의 hello 배포를 클릭 하 고 **모든 설정을**, 클릭 하 고 **속성**합니다.
* 에 Azure 클래식 포털 hello 클라우드 서비스의 hello 배포를 클릭 하 고 **대시보드**hello 페이지의 hello 오른쪽 아래 모서리에 있는 (아래 **눈에 보는**). 이 창에 대한 "속성" 레이블이 없습니다.

> [!NOTE]
> Hello의 hello 내용을 복사할 수는 있지만 **속성** hello hello 창 오른쪽 위 모서리에 hello 아이콘을 클릭 하 여 창 toohello 클립보드 합니다.
>
>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="problem-i-cannot-access-my-website-but-my-deployment-is-started-and-all-role-instances-are-ready"></a>문제: 내 배포가 시작되고 모든 역할 인스턴스가 준비되었지만 내 웹 사이트에 액세스할 수가 없어요
hello 웹 사이트 URL 링크 hello 포털에 표시 된 hello 포트를 포함 하지 않습니다. 웹 사이트에 대 한 hello 기본 포트는 80입니다. 다른 포트에서 구성 된 toorun 응용 프로그램을 사용 하는 경우 hello 웹 사이트에 액세스할 때 hello 올바른 포트 번호 toohello URL에 추가 해야 합니다.

1. Hello Azure 포털에서에서 클라우드 서비스의 hello 배포를 클릭 합니다.
2. Hello에 **속성** hello 역할 인스턴스에 대 한 hello 포트를 확인 하는 hello Azure 포털의 창 (아래 **입력 끝점**).
3. Hello 포트 80 없으면 hello 응용 프로그램에 액세스할 때 hello 올바른 포트 값 toohello URL을 추가 합니다. toospecify 기본이 아닌 포트 공백 없이 hello 포트 번호 뒤에 오는 콜론 (:) 다음 hello URL을 입력 합니다.

## <a name="problem-my-role-instances-recycled-without-me-doing-anything"></a>문제: 아무 것도 하지 않았는데 내 역할 인스턴스가 재활용되었어요
서비스 복구는 Azure에서 문제 노드를 검색 하 고 따라서 역할 인스턴스 toonew 노드를 이동 하는 경우 자동으로 발생 합니다. 이 경우 역할 인스턴스가 자동으로 재활용될 수 있습니다. 했는지 toofind 서비스 오류가 발생 했습니다 복구:

1. Hello Azure 포털에서에서 클라우드 서비스의 hello 배포를 클릭 합니다.
2. Hello에 **속성** hello Azure 포털의 창 hello 정보를 검토 하 고 hello 역할 재활용을 관찰 하는 hello 시간 동안 발생 한 서비스 복구 것인지 확인 합니다.

또한 역할은 호스트 OS와 게스트 OS를 업데이트하는 동안 대략 한 달에 한 번 정도 재활용합니다.  
자세한 내용은 hello 블로그 게시물을 참조 하십시오. [tooOS 업그레이드를 다시 시작 인 한 역할 인스턴스](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx)

## <a name="problem-i-cannot-do-a-vip-swap-and-receive-an-error"></a>문제: VIP 교환을 수행하고 오류를 받을 수 없어요
배포 업데이트가 진행 중인 경우 VIP 교환이 허용되지 않습니다. 배포 업데이트가 다음과 같은 경우 자동으로 발생할 수 있습니다.

* 새 게스트 운영 체제를 사용할 수 있고 자동 업데이트를 구성합니다.
* 서비스 복구가 수행됩니다.

out toofind 자동 업데이트 하는 경우로 인해 VIP 교체를 수행:

1. Hello Azure 포털에서에서 클라우드 서비스의 hello 배포를 클릭 합니다.
2. Hello에 **속성** hello Azure 포털의 창 hello 값을 살펴보고 **상태**합니다. 이 경우 **준비**, 다음 확인 **마지막 작업** toosee 최근에 발생 한 경우에 hello VIP swap 하지 못할 수 있습니다.
3. Hello 프로덕션 배포에 대 한 1 및 2 단계를 반복 합니다.
4. 자동 업데이트 프로세스에 있으면 대기 동안 toodo hello VIP 교체 하기 전에 toofinish 합니다.

## <a name="problem-a-role-instance-is-looping-between-started-initializing-busy-and-stopped"></a>문제: 역할 인스턴스가 시작됨, 초기화 중, 사용 중 및 중지됨 사이를 반복해요
이 상태는 응용 프로그램 코드, 패키지 또는 구성 파일에 문제가 있음을 나타낼 수 있습니다. 이 경우 몇 분 마다 변경 수 toosee hello 상태 수 있으며 hello Azure 포털 이라는 메시지가 표시와 같은 **재활용**, **Busy**, 또는 **Initializing**합니다. 이 hello 역할 인스턴스가 실행에서 상태를 유지 하는 hello 응용 프로그램 문제가 된다는 것을 의미 합니다.

방법에 대 한 자세한 내용은 hello 블로그 게시물을 참조 하는이 문제에 대 한 tootroubleshoot [Azure PaaS 계산 진단 데이터](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx) 및 [일반적인 문제가 그 원인 역할 toorecycle](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md)합니다.

## <a name="problem-my-application-stopped-working"></a>문제: 내 응용 프로그램의 작동이 중지되었어요
1. Azure 포털 hello hello 역할 인스턴스를 클릭 합니다.
2. Hello에 **속성** hello Azure 포털의 창 hello 조건 tooresolve 다음 문제를 고려 합니다.
   * Hello 역할 인스턴스가 최근에 중지 된 경우 (의 hello 값을 확인할 수 있습니다 **중단 횟수**), hello 배포를 업데이트할 수 있습니다. Hello 역할 인스턴스는 자체에서 작동 하 고 다시 시작 하면 toosee를 기다립니다.
   * Hello 역할 인스턴스가 **Busy**, 응용 프로그램 코드 toosee 경우 확인 hello [StatusCheck](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.statuscheck) 이벤트를 처리 합니다. 이 이벤트를 처리 하는 일부 코드를 수정 또는 tooadd 할 수 있습니다.
   * Hello 진단 데이터를 통해 이동 하 고 문제 해결 시나리오 hello 블로그 게시물에서 [Azure PaaS 계산 진단 데이터](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)합니다.

> [!WARNING]
> 클라우드 서비스를 재활용 하는 경우 다시 설정 hello 배포에 대 한 hello 속성 지워집니다 hello 원래 문제에 대 한 hello 정보입니다.
>
>

## <a name="next-steps"></a>다음 단계
클라우드 서비스에 대한 [문제해결 문서](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) 를 더 봅니다.

Azure PaaS 컴퓨터 진단 데이터를 사용 하 여 tootroubleshoot 클라우드 서비스 역할을 발급 하는 방법을 toolearn 참조 [Kevin Williamson 블로그 시리즈](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)합니다.
