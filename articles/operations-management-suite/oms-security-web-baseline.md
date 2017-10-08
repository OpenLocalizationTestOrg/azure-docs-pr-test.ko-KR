---
title: "관리 도구 모음 보안 및 감사 솔루션 웹 초기 aaaOperations | Microsoft Docs"
description: "이 문서에서는 설명 어떻게 toouse OMS 보안 및 감사 솔루션 tooperform 규정 준수 및 보안 용도 대 한 모든 모니터링 대상된 웹 서버에 대 한 웹 초기 평가 합니다."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ROBOTS: NOINDEX
redirect_url: https://www.microsoft.com/cloud-platform/security-and-compliance
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: 8aa87fa404ff97ab549dda3f9bebb75766055963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a>Operations Management Suite 보안 및 감사 솔루션의 웹 기준 평가
이 문서를 사용 하면 toouse [Operations Management Suite (OMS) 보안 및 감사 솔루션](operations-management-suite-overview.md) 웹 기능 tooaccess hello 보안 리소스 상태를 모니터링 하는 초기 평가 합니다.

## <a name="what-is-web-baseline-assessment"></a>웹 기준 평가란?
현재 OMS 보안은 운영 체제에 대한 보안 기준 평가를 제공합니다. 24 시간 마다 서버 운영 체제 설정을 hello를 검색 하 고 잠재적으로 취약 한 설정에 대 한 뷰를 제공 합니다. 이에 대한 자세한 내용은 [Operations Management Suite 보안 및 감사 솔루션의 기준 평가](oms-security-baseline.md)를 참조하세요.

hello hello 웹 초기 평가의 ´ ֲ toofind 잠재적으로 취약 한 웹 서버 설정. hello 웹 초기 구성에 대 한 기본 원본은 다음 세 가지 hello:.NET, ASP.NET 및 IIS 구성 합니다.  운영 시스템 초기 평가 hello, 처럼 OMS 보안은 사용 하겠습니다 tooscan 사용자 웹 서버에 24 시간 마다 하 고 그 중 보안 상태에 대 한 뷰를 제공 합니다.  인터넷 정보 서비스 (IIS), 구성은 하는 고도로 사용자 지정 가능한 재정의 된 다양 한 사이트 및 응용 프로그램 수준 toobe 수 있습니다. hello 스캐너 추가 toohello 기본 루트 수준에서 각 응용 프로그램/사이트 수준에서 hello 설정을 확인합니다. 이 tooidentify 잠재적인 취약점 설정 위치를 사용 하면 고 신속 하 게 재구성 합니다.


## <a name="web-security-baseline-assessment"></a>웹 보안 기준 평가
이 미리 보기에 대 한이 기능은 toobe hello OMS 검색 옵션을 사용 하 여 액세스 하려고 합니다. Tooperform appropriated hello 쿼리 아래 hello 단계를 수행 합니다.

1. Hello에 **Microsoft Operations Management Suite** 기본 대시보드 클릭 **보안 및 감사** 바둑판식으로 배열입니다.
2. Hello에 **보안 및 감사** 대시보드를 클릭 하 여 **로그 검색** 단추입니다.
3. 사용할 수 있는 hello 첫 번째 쿼리는 hello **웹 초기 평가 요약**합니다. Hello에 **검색 시작** 필드에서이 쿼리를 입력: 형식*SecurityBaselineSummary BaselineType = 웹 =*합니다. hello 화면에 다음 출력 예제에 있습니다.

![웹 기준 평가 요약](./media/oms-security-web-baseline/oms-security-web-baseline-fig1-new.png)

> [!NOTE]
> 이 쿼리에서 각 레코드는 단일 서버에 대한 요약 평가를 나타냅니다.

Hello에 있는 경우 **로그 검색**을 각각 다른 쿼리에 tooobtain hello 웹 초기 평가 대 한 자세한 정보를 입력할 수 있습니다. 또한 toohello 이전 쿼리를 사용할 수도 있습니다 hello이 미리이 보기에는 스토리를 수행 합니다.

**웹 기준 규칙 평가**: 각 레코드는 단일 서버에서 단일 웹 기준 규칙 평가를 나타냅니다. Hello 규칙과 위치, hello 예상 결과 hello 실제 결과 대 한 모든 데이터를 포함 합니다.

**쿼리**: Type*=SecurityBaseline BaselineType=web*

![웹 기준 규칙 평가](./media/oms-security-web-baseline/oms-security-web-baseline-fig2.png)

**특정 서버에 대 한 모든 결과 표시**:이 쿼리에서 toosee 발생 하는 방법을 보여 줍니다. 특정 서버입니다.

**쿼리**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*

![모든 결과](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

이러한 레코드/쿼리 toocreate 고유한 대시보드, 보고서 또는 경고에도 사용할 수 있습니다. hello 화면 아래에 샘플 UI 컨트롤이 tooyour 대시보드를 추가할 수 있습니다. 학습할 수 있는 방법을 toovisualize OMS 뷰 디자이너를 사용 하 여 데이터 [여기](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/)합니다. hello 아래 화면은이 사용자 지정 확인 되 면 hello 타일 방법의 예는 같습니다.

![샘플 UI](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

> [!NOTE]
> 다운로드할 수 있습니다 hello 초기 평가 대 한 체크 인 된 tooknow hello 설정, 원하는 경우 [이 Excel 스프레드시트](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) 이러한 설정을 포함 하 합니다.

## <a name="see-also"></a>참고 항목
이 문서에서는 OMS 보안 및 감사 웹 기준 평가에 대해 알아보았습니다. OMS 보안에 대해 자세히 toolearn hello 다음 문서 참조:

* [OMS(Operations Management Suite) 개요](operations-management-suite-overview.md)
* [모니터링 및 Operations Management Suite 보안 및 감사 솔루션에 응답 중 tooSecurity 경고](oms-security-responding-alerts.md)
* [Operations Management Suite 보안 및 감사 솔루션의 리소스 모니터링](oms-security-monitoring-resources.md)

