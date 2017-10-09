---
title: "Azure 보안 센터에서 보안 경고 aaaHandling | Microsoft Docs"
description: "이 문서 toouse Azure 보안 센터 기능 toohandle 보안 사고 수 있습니다."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: e8feb669-8f30-49eb-ba38-046edf3f9656
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: edb911c298a2ce93cd0ea5b22ce002005040090f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="handling-security-incidents-in-azure-security-center"></a>Azure Security Center에서 보안 인시던트 처리
에 대 한 심사 및 보안 경고를 조사 숙련 보안 분석가 hello에 대 한 시간이 걸릴 수 있으며 여러 하드 tooeven 위치를 알 수는 toobegin 합니다. 사용 하 여 [분석](security-center-detection-capabilities.md) 고유 간에 tooconnect hello 정보 [보안 경고](security-center-managing-and-responding-alerts.md), 보안 센터 공격 캠페인의 단일 뷰를 제공할 수 있습니다 및 관련 된 모든 hello 경고-할 수 있습니다 어떤 작업 hello 공격자는 적용 하 고 리소스에 영향을 받은 신속 하 게 이해 합니다.

이 문서에서는 어떻게 toouse 보안 경고의 보안 센터 tooassist 기능 보안 문제를 처리 합니다.

## <a name="what-is-a-security-incident"></a>보안 인시던트란?
보안 센터에서 보안 인시던트는 [kill 체인](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) 패턴과 일치하는 리소스에 대한 모든 경고의 집계입니다. Hello에 인시던트 표시 [보안 경고](security-center-managing-and-responding-alerts.md) 타일 및 블레이드입니다. 인시던트 각 항목에 대 한 자세한 내용은 tooobtain 있습니다 수 있도록 하는 hello 목록이 관련된 경고를 표시 합니다.

## <a name="managing-security-incidents"></a>보안 인시던트 관리
Hello 보안 경고 타일 확인 하 여 현재 보안 인시던트를 검토할 수 있습니다. Hello Azure 포털에 액세스 하 고 각 보안 문제에 대 한 자세한 내용은 아래 toosee hello 단계를 수행 합니다.

1. Hello 보안 센터 대시보드에서 hello 나타납니다 **보안 경고** 바둑판식으로 배열입니다.

    ![보안 센터의 보안 경고 타일](./media/security-center-incident/security-center-incident-fig1.png)

2. 이 타일 tooexpand 클릭할 한 경우 보안 문제가 감지 되 면 아래와 같이 hello 보안 경고 그래프 아래에 표시 됩니다.

    ![보안 인시던트](./media/security-center-incident/security-center-incident-fig2.png)

3. Hello 보안 문제 설명에 아이콘은 tooother 경고를 비교 합니다. 클릭 하 여 조치 tooview이이 인시던트에 대 한 더 자세히 설명 합니다.

    ![보안 인시던트](./media/security-center-incident/security-center-incident-fig3.png)

4. Hello에 **인시던트** 현재 상태의 전체 설명 (경우에이 높은)의 심각도 포함 하는이 보안 사고에 대 한 세부 정보 블레이드에서 더 표시 됩니다 (이 경우 이것이 여전히 *활성*hello 사용자를 의미 있는 작업 tooit 수행 하지 않은-hello에서 hello 인시던트를 마우스 오른쪽 단추로 클릭 하 여이 작업을 수행할 수 있습니다, **보안 경고** 블레이드), hello 공격 리소스 (이 경우 *VM1*), hello 인시던트에 대 한 업데이트 관리 단계가 hello 및이 서비스에 포함 된 hello 경고가 hello 아래쪽 창에 있는 합니다. 각 경고에 대 한 자세한 내용은 tooobtain 하려는 경우 아래와 같이 다른 블레이드를 클릭 하기만 열 됩니다.

    ![보안 인시던트](./media/security-center-incident/security-center-incident-fig4.png)

이 블레이드는 hello 방법은 toohello 경고에 따라 달라 집니다. 읽기 [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) 방법에 대 한 자세한 내용은 toomanage 이러한 경고 합니다. 이 기능에 대한 몇 가지 중요한 고려 사항은 다음과 같습니다.

* 새 필터를 사용 하면 toocustomize 보기 tooIncident만만, 경고 또는 둘 다 있습니다.
* hello 동일한 경고에서는 인시던트 (있는 경우)는 물론 toobe 독립 실행형 경고로 표시의 일부로 존재할 수 있습니다.

## <a name="see-also"></a>참고 항목
이 문서에서는 toouse 보안 센터에서 인시던트 기능 보안 hello 하는 방법을 배웠습니다. 보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.

* [관리 하 고 Azure 보안 센터에서 toosecurity 경고 응답](security-center-managing-and-responding-alerts.md)
* [Azure 보안 센터 감지 기능](security-center-detection-capabilities.md)
* [Azure Security Center 계획 및 작업 가이드](security-center-planning-and-operations-guide.md)
* [관리 하 고 Azure 보안 센터에서 toosecurity 경고 응답](security-center-managing-and-responding-alerts.md)
* [Azure 보안 센터 FAQ](security-center-faq.md)-찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/)--Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.
