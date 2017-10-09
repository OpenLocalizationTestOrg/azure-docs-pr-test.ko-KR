---
title: "보안 센터 위협 인텔리전스 보고서 aaaAzure | Microsoft Docs"
description: "이 문서를 사용 하면 toouse Azure 보안 센터 위협 지능형 보고서 조사 toofind 하는 동안 보안 경고에 대 한 자세한 정보."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 5662e312-e8c2-4736-974e-576eeb333484
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: c888cfac1dd8b057616a6b8e6c6f6b67b552f2e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-threat-intelligence-report"></a>Azure Security Center 위협 인텔리전스 보고서
이 문서에서는 Azure Security Center 위협 인텔리전스 보고서를 사용하여 보안 경고를 생성한 위협에 관한 자세한 정보를 확인하는 방식에 대해 설명합니다.

## <a name="what-is-a-threat-intelligence-report"></a>위협 인텔리전스 보고서란?
보안 센터 위협 요소 탐지 Azure 리소스, hello 네트워크와 연결 된 파트너 솔루션의 보안 정보를 모니터링 하 여 작동 합니다. 이 정보를 종종 tooidentify 위협 여러 소스의 정보 상관 관계를 분석 합니다. 이 프로세스는 hello 보안 센터의 일부 [검색 기능이](security-center-detection-capabilities.md)합니다.

Security Center에서 위협을 식별하면 [보안 경고](security-center-managing-and-responding-alerts.md)를 트리거하며, 여기에는 수정 제안을 포함하여 특정 이벤트와 관련된 자세한 정보가 포함되어 있습니다. 보안 센터 등의 정보를 비롯 하 여 검색 된 hello 위협에 대 한 정보를 포함 하는 위협 인텔리전스 보고서에 포함 되어 tooassist 사고 대응 팀 조사 및 재구성 위협은:

* 공격자의 ID 또는 연결(이 정보가 제공되는 경우)
* 공격자의 목표
* 현재 및 과거 공격 캠페인(이 정보가 제공되는 경우)
* 공격자의 전술, 도구 및 프로시저
* URL, 파일 해시 등 관련 IoC(보안 침해 지표)
* Hello 업계 및 지리적 널리 tooassist victimology 위험이 있습니다. Azure 리소스 하는지 여부를 확인 하면
* 마이그레이션 및 수정 정보

> [!NOTE]
> 특정 보고서의 정보 양을 hello 달라 집니다. hello 수준의 세부 정보는 hello 맬웨어 활동 및 보급을 기반으로 합니다.
>
>

보안 센터에 세 가지 유형의 toohello 공격에 따라 다를 수 있는 위협 보고서 있습니다. 사용할 수 있는 hello 보고서에는

* **그룹 활동 보고서** - 공격자 및 이들의 목표와 전술에 대해 자세히 설명합니다.
* **캠페인 보고서**: 특정 공격 캠페인의 세부 정보에 중점을 둡니다.
* **요약 보고서 위협**: hello에 모든 항목의 hello 이전 두 보고서에 설명 합니다.

Hello 하는 동안 이러한 종류의 정보는 매우 유용 [사고 대응](security-center-incident-response.md) hello 공격, hello 공격자의 동기 및 작업의 진행 중인 조사 toounderstand hello 소스는 프로세스 toodo toomitigate이 문제를 앞으로 이동 합니다.

## <a name="how-tooaccess-hello-threat-intelligence-report"></a>어떻게 tooaccess 위협 인텔리전스 보고서 hello?
Hello 확인 하 여 현재 경고를 검토할 수 있습니다 **보안 경고** 바둑판식으로 배열입니다. Hello Azure 포털을 열고 각 경고에 대 한 자세한 내용은 아래 toosee hello 단계를 수행 합니다.

1. Hello 보안 센터 대시보드에서 hello 나타납니다 **보안 경고** 바둑판식으로 배열입니다.
2. Hello 타일 tooopen hello 클릭 **보안 경고** 블레이드 hello 경고에 대 한 자세한 내용은 포함 된 추가 정보를 원하는 tooobtain hello 보안 경고가 클릭에 대 한 합니다.

    ![보안 경고](./media/security-center-threat-report/security-center-threat-report-fig1.png)
3. 이 경우 hello **실행 된 의심 스러운 프로세스** 블레이드 아래 hello 그림에 나와 있는 것 처럼 hello 경고에 대 한 hello 세부 정보를 표시 합니다.:

    ![보안 경고 세부 정보](./media/security-center-threat-report/security-center-threat-report-fig2.png)
4. 각 보안 경고에 대해 사용할 수 있는 정보의 양을 hello 경고 toohello 유형에 따라 달라 집니다. Hello에 **보고서** 링크 toohello 위협 인텔리전스 보고서 필드입니다. 해당 링크를 클릭하면 다른 브라우저 창에서 PDF 파일을 표시합니다.

   ![저장소 선택](./media/security-center-threat-report/security-center-threat-report-fig3.png)

여기에서 hello이 보고서와을 발급할 보안 hello에 대 한 자세한 읽기에 대 한 PDF 검색 되었습니다를 다운로드 하 고 제공 하는 hello 정보에 따라 동작을 수행할 수입니다.

## <a name="see-also"></a>참고 항목
이 문서에서는 보안 경고에 대해 조사하는 중에 Azure Security Center 위협 인텔리전스 보고서를 사용 방법을 살펴보았습니다. Azure 보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.

* [Azure Security Center FAQ](security-center-faq.md)로 설정합니다. Hello 서비스를 사용 하는 방법에 대 한 질문과 대답을 찾습니다.
* [사고 대응에 Azure Security Center 활용](security-center-incident-response.md)
* [Azure Security Center 감지 기능](security-center-detection-capabilities.md)
* [Azure Security Center planning and operations guide](security-center-planning-and-operations-guide.md)로 설정합니다. 자세한 내용은 방법 tooplan hello 디자인 고려 사항 tooadopt Azure 보안 센터를 이해 하 고 있습니다.
* [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md)합니다. 자세한 내용은 방법 toomanage 및 응답 toosecurity 경고 합니다.
* [Azure 보안 센터에서 보안 인시던트 처리](security-center-incident.md)
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/). Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.
