---
title: "보안 센터와 로그 통합 aaaAzure | Microsoft Docs"
description: "어떻게 tooget Azure 보안 센터 로그 통합을 사용 하는 경고에 알아봅니다"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 03/22/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: bcc208d071ec03738215f2aee3b71c7b10927904
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-your-security-center-alerts-in-azure-log-integration"></a>어떻게 tooget 보안 센터에서에서 경고를 Azure 로그 통합
이 문서에서는 hello 단계 필요한 tooenable hello Azure 로그 통합 서비스 toopull Azure 보안 센터에서 생성 되는 보안 경고 정보를 제공 합니다. 성공적으로 완료 해야 hello의 hello 단계 [시작](security-azure-log-integration-get-started.md) 이 문서의 hello 단계를 수행 하기 전에 문서.

## <a name="detailed-steps"></a>자세한 단계
hello 다음 단계 만들어집니다 hello 필요한 Azure Active Directory 서비스 사용자 및 서비스 원칙 할당 hello 읽기 권한을 toohello 구독:
1. Hello 명령 프롬프트를 열고 너무 이동**c:\Program Files\Microsoft Azure 로그 통합**
2. Hello 명령 실행``azlog createazureid``

    이 명령은 사용자에게 Azure 로그인을 요구합니다. hello 명령은 다음 만듭니다는 [Azure Active Directory 서비스 사용자](../active-directory/develop/active-directory-application-objects.md) hello에서 호스팅하는 Azure AD 테 넌 트 hello 로그인 한 사용자는 hello에는 관리자, 공동 관리자 또는 소유자는 Azure 구독. hello 로그인 한 사용자가 게스트 사용자를 hello Azure AD 테 넌 트에에서만 hello 명령이 실패 합니다. 인증 tooAzure는 통해 Azure AD (Active Directory)를 수행 됩니다. Azlog 통합에 대 한 서비스 사용자를 만들면 hello Azure 구독에서 액세스 tooread 제공 될 Azure AD id 만들어집니다.

2. 그런 다음 2 단계에서 만든 hello 구독 toohello 서비스 사용자에 대 한 판독기 액세스를 할당 하는 명령을 실행 합니다. 구독 Id를 지정 하지 않으면 hello 명령 tooassign hello 서비스 주 판독기 역할 tooall 구독 toowhich 모든 액세스할 수 있는 시도 합니다. </br></br>
``azlog authorize <SubscriptionID>`` </br> 예제: </br>
``azlog authorize 0ee55555-0bc4-4a32-a4e8-c29980000000``

    >[!NOTE]
    Hello를 실행 하는 경우 경고를 표시 될 수 있습니다 hello createazureid 명령 후 즉시 명령에 권한을 부여 합니다. Hello Azure AD 계정이 만들어질 때와 hello 계정에 사용 하기 위해 제공 된 경우 간에 약간의 대기 시간이 있습니다. 에 대 한 대기 hello createazureid 명령 toorun hello를 실행 한 후 60 초 명령에서 권한을 부여할 경우 이러한 경고가 표시 되지 않습니다.

4. 감사 로그 JSON 파일 hello 폴더 tooconfirm 다음 hello 사항이 확인 합니다.
 * **c:\Users\azlog\AzureResourceManagerJson**
 * **c:\Users\azlog\AzureResourceManagerJsonLD** </br></br>
5. 보안 센터 알림을에 존재 하는 폴더 tooconfirm 다음 hello를 확인 합니다.</br></br>
 * **c:\Users\azlog\AzureSecurityCenterJson**
 * **c:\Users\azlog\AzureSecurityCenterJsonLD** </br></br>

Hello 설치 및 구성 하는 동안 모든 문제를 실행 하면을 개시 하세요는 [지원 요청](/azure-supportability/how-to-create-azure-support-request.md)선택, **로그 통합** 지원을 요청 하는 hello 서비스로 합니다.

## <a name="next-steps"></a>다음 단계
Azure 로그 통합에 대해 자세히 toolearn hello 다음 문서를 참조 하십시오.

* [Azure 로그에 대한 Microsoft Azure 로그 통합](https://www.microsoft.com/download/details.aspx?id=53324) – Azure 로그 통합에 대한 세부 정보, 시스템 요구 사항 및 설치 지침을 다운로드할 수 있습니다.
* [소개 tooAzure 로그 통합](security-azure-log-integration-overview.md) -이 문서에서는 소개 tooAzure 로그 통합의 주요 기능 및 작동 방식입니다.
* [구성 단계를 파트너](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) –이 블로그 게시물을 보면 tooconfigure Azure Splunk, HP ArcSight 및 IBM QRadar 파트너 솔루션과 통합 toowork를 로그 하는 방법은 합니다.
* [Azure 로그 통합 FAQ(질문과 대답)](security-azure-log-integration-faq.md) - 이 FAQ는 Azure 로그 통합에 대한 질문에 답변합니다.
* [보안 센터를 통합 합니다. Azure와 경고 로그 통합](../security-center/security-center-integrating-alerts-with-log-integration.md) -이 문서에서는 어떻게 toosync 보안 센터 경고, 로그 분석으로 Azure 진단 및 Azure 감사 로그에서 수집 하는 가상 컴퓨터 보안 이벤트와 함께 또는 SIEM 솔루션입니다.
* [Azure 진단 및 Azure 감사 로그에 대 한 새로운 기능](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/) –이 블로그 게시물 tooAzure 감사 로그를 소개 하 고 Azure 리소스의 hello 작업을 파악할 수 있는 기타 기능입니다.
