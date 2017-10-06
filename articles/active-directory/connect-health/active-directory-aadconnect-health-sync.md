---
title: "동기화 하는 Azure AD Connect Health aaaUsing | Microsoft Docs"
description: "이 hello Azure AD Connect Health 페이지 toomonitor Azure AD Connect 동기화 하는 방법에 대해 설명 합니다."
services: active-directory
documentationcenter: 
author: karavar
manager: femila
ms.assetid: 1dfbeaba-bda2-4f68-ac89-1dbfaf5b4015
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 56f0582be30e664026cedf15350bc23501998bfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-ad-connect-sync-with-azure-ad-connect-health"></a>Azure AD Connect Health를 사용하여 Azure AD Connect 동기화 모니터링
hello 설명서는 특정 toomonitoring Azure AD Connect Health를 사용 하 여 Azure AD 연결 (동기화)입니다.  Azure AD Connect Health와 함께 AD FS 모니터링에 대한 내용은 [AD FS와 함께 Azure AD Connect Health 사용](active-directory-aadconnect-health-adfs.md)을 참조하세요. 또한 Azure AD Connect Health와 함께 Active Directory 도메인 서비스를 모니터링하는 방법에 대한 정보는 [AD DS와 함께 Azure AD Connect Health 사용](active-directory-aadconnect-health-adds.md)을 참조하세요.

![동기화에 대한 Azure AD Connect Health](./media/active-directory-aadconnect-health-sync/sync-blade.png)

## <a name="alerts-for-azure-ad-connect-health-for-sync"></a>동기화에 대한 Azure AD Connect Health에 대한 경고
hello Azure AD Connect Health 경고 동기화 섹션에 대 한 활성 경고 목록이 hello를 제공 합니다. 각 경고 관련 정보, 해결 단계 및 toorelated 설명서 링크를 포함합니다. 활성 또는 해결 된 경고를 선택 하 여 추가 정보 뿐만 아니라 tooresolve hello 경고 및 링크 tooadditional 설명서를 수행할 수 있는 단계는 새 블레이드가 표시 됩니다. 또한 hello 과거에 해결 된 경고에 기록 데이터를 볼 수 있습니다.

단계 뿐만 아니라 추가 정보 제공 되는 경고를 선택 하 여 수행할 수 tooresolve hello 경고 및 링크 tooadditional 설명서입니다.

![Azure AD Connect 동기화 오류](./media/active-directory-aadconnect-health-sync/alert.png)

### <a name="limited-evaluation-of-alerts"></a>제한된 경고 평가
Azure AD Connect (예: 특성 필터링 hello 기본 구성 tooa 사용자 지정 구성에서 변경 된 경우) hello 기본 구성을 사용 하지 않으면, 다음 hello Azure AD Connect Health agent는 업로드 하지 hello 오류 이벤트에 대 한 관련된 tooAzure AD 연결 합니다.

이 경고의 hello 평가 hello 서비스에 의해 제한 됩니다. 서비스에서 hello Azure 포털에서에서이 문제를 나타내는 배너를 나타납니다 합니다.

![동기화에 대한 Azure AD Connect Health](./media/active-directory-aadconnect-health-sync/banner.png)

"설정"을 클릭 하 고 Azure AD Connect Health agent tooupload 모든 오류 로그를 허용 하 여이 변경할 수 있습니다.

![동기화에 대한 Azure AD Connect Health](./media/active-directory-aadconnect-health-sync/banner2.png)

## <a name="sync-insight"></a>동기화 정보
Admins 자주 tooknow hello 시간이 toosync 변경 tooAzure AD 및 hello 양의 변화에 대 한 합니다. 이 기능을 통해 쉽게 toovisualize이 그래프 아래의 hello를 사용 하 여:   

* 동기화 작업의 대기 시간
* 개체 변경 추세

### <a name="sync-latency"></a>동기화 대기 시간
이 기능은 hello 동기화 (가져오기, 내보내기 등)에 대 한 작업 커넥터의 대기 시간의 그래픽 추세를 제공합니다.  빠른 하며 쉽게 toounderstand 조사 해야 하는 hello 대기 시간 (큰 발생 한 변경 집합이 있는 경우 더 큰) 작업 뿐만 아니라 방식으로 toodetect 비정상의 대기 시간을 뿐만 아니라 hello.

![동기화 대기 시간](./media/active-directory-aadconnect-health-sync/synclatency02.png)

기본적으로 hello hello Azure AD 커넥터에 대 한 작업 'Export' hello 대기 시간만 표시 됩니다.  toosee hello 커넥터에는 다양 한 작업 또는 tooview 작업에서 다른 커넥터를 마우스 오른쪽 단추로 클릭 hello 차트에서 차트 편집를 선택 하거나 hello "대기 시간 차트 편집" 단추를 클릭 하 고 hello 특정 작업 및 커넥터를 선택 합니다.

### <a name="sync-object-changes"></a>동기화 개체 변경 사항
이 기능은 hello 계산 하 고 AD tooAzure 내보내집니다 변경 내용 수의 그래픽 추세를 제공 합니다.  오늘날, 동안 toogather hello 동기화 로그에서이 정보는 어렵습니다.  hello 차트 제공, 보다 간단한 방법을 뿐만 아니라 사용자 환경에서 발생 하는 변경 내용 hello 수 뿐만 아니라 발생 하는 hello 오류의 시각적 보기를 모니터링 합니다.

![동기화 대기 시간](./media/active-directory-aadconnect-health-sync/syncobjectchanges02.png)

## <a name="object-level-synchronization-error-report-preview"></a>개체 수준 동기화 오류 보고서(미리 보기)
이 기능은 Azure AD Connect를 사용하여 Windows Server AD와 Azure AD 간의 ID 데이터를 동기화할 때 발생할 수 있는 동기화 오류에 대한 보고서를 제공합니다.

* hello 보고서에서는 오류 hello 동기화 클라이언트 (Azure AD Connect 버전 1.1.281.0 또는 이상)
* Hello hello 동기화 엔진에서 마지막 동기화 작업의 hello 발생 한 오류를 포함 합니다. ("Export" hello Azure AD 커넥터에서.)
* 동기화 용 azure AD Connect Health agent hello 보고서 tooinclude hello 최신 데이터에 대 한 아웃 바운드 연결 필요한 toohello 시작점과 끝점이 있어야 합니다.
* hello 보고서가 **매 30 분 후 업데이트 된** 동기화 용 Azure AD Connect Health agent가 업로드 hello 데이터를 사용 하 여 합니다. 주요 기능을 수행 하는 hello 제공

  * 오류 분류
  * 범주별 오류에 따른 개체의 목록
  * 한 곳에서 발생 한 hello 오류에 대 한 모든 hello 데이터
  * 오류로 인해 tooa 충돌 개체의 특징이 비교 정렬
  * (출시 예정) CVS로 hello 오류 보고서를 다운로드 합니다.

### <a name="categorization-of-errors"></a>오류 분류
hello 보고서 hello 기존 동기화 오류 범주를 수행 하는 hello에서 분류 합니다.

| Category | 설명 |
| --- | --- |
| 중복 특성 |proxyAddresses, UserPrincipalName 같은 테넌트 내에서 고유해야 하는 Azure AD에서 하나 이상의 특성의 값이 중복된 개체를 만들거나 업데이트하려고 시도할 때의 오류 |
| 데이터 불일치 |Hello 소프트 일치 toomatch 개체 동기화 오류를 일으키는 실패 한 경우 오류가 발생 했습니다. |
| 데이터 유효성 검사 실패 |UserPrincipalName, 등의 중요 한 특성에서 지원 되지 않는 문자가 같은 tooinvalid 데이터 않아서 발생 한 오류에는 Azure AD에 기록 되기 전에 유효성 검사가 실패 하는 오류 형식을 따릅니다. |
| 큰 특성 |하나 이상의 특성 hello 보다 큰 경우 오류 크기, 길이 또는 수를 허용 합니다. |
| 기타 |모든 다른 오류 범주 위에 hello에 맞지 않는입니다. 의견에 따라 이 범주는 하위 범주로 분할됩니다. |

![동기화 오류 보고서 요약](./media/active-directory-aadconnect-health-sync/errorreport01.png)
![동기화 오류 보고서 범주](./media/active-directory-aadconnect-health-sync/errorreport02.png)

### <a name="list-of-objects-with-error-per-category"></a>범주별 오류에 따른 개체의 목록
각 범주를 드릴링 하는 hello 오류 해당 범주에 포함 된 개체의 hello 목록을 제공 합니다.
![동기화 오류 보고서 목록](./media/active-directory-aadconnect-health-sync/errorreport03.png)

### <a name="error-details"></a>오류 세부 정보
다음 데이터는 hello에서 사용할 수 있는 각 오류에 대 한 보기를 설명 합니다.

* Hello에 대 한 식별자 *AD 개체* 참여
* Hello에 대 한 식별자 *Azure AD 개체* (로) 참여
* 오류 설명 및 방법을 toofix
* 관련 문서

![동기화 오류 보고서 세부 정보](./media/active-directory-aadconnect-health-sync/errorreport04.png)

### <a name="download-hello-error-report-as-csv"></a>Hello 오류 보고서를 CSV로 다운로드
Hello를 선택 하 여 "내보내기" 단추 모든 hello 오류에 대 한 모든 hello 세부 정보가 된 CSV 파일을 다운로드할 수 있습니다.

## <a name="related-links"></a>관련 링크
* [동기화 중 오류 문제 해결](../connect/active-directory-aadconnect-troubleshoot-sync-errors.md)
* [중복 특성 복원력](../connect/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Azure AD Connect Health Agent 설치](active-directory-aadconnect-health-agent-install.md)
* [Azure AD Connect Health 작업](active-directory-aadconnect-health-operations.md)
* [AD FS와 함께 Azure AD Connect Health 사용](active-directory-aadconnect-health-adfs.md)
* [AD DS와 함께 Azure AD Connect Health 사용](active-directory-aadconnect-health-adds.md)
* [Azure AD Connect Health FAQ](active-directory-aadconnect-health-faq.md)
* [Azure AD Connect Health 버전 내역](active-directory-aadconnect-health-version-history.md)