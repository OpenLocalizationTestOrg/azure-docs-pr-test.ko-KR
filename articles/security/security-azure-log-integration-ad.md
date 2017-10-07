---
title: "Azure Active Directory 감사 로그와 로그 통합 aaaAzure | Microsoft Docs"
description: "Tooinstall hello Azure 로그 통합 서비스 하 고 Azure 감사 로그에서 로그를 통합 하는 방법에 대해 알아봅니다"
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
ms.date: 08/08/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: 3ee8fa3b8b5e9bd33202e57ed5327cd8d3127f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-audit-logs"></a>Azure Active Directory 감사 로그 통합

Azure AD(Azure Active Directory) 감사 이벤트를 통해 Azure Active Directory에서 발생한 권한 있는 작업을 식별할 수 있습니다. 이벤트를 검토 하 여 추적할 수 있는 hello 형식을 볼 수 있습니다 [Azure Active Directory 감사 보고서 이벤트](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md)합니다.

> [!NOTE]
> 이 문서의 hello 단계를 시도 하기 전에 hello 검토 해야 [시작](security-azure-log-integration-get-started.md) 문서 및 hello 단계를 완료 합니다.

## <a name="steps-toointegrate-azure-active-directory-audit-logs"></a>단계 toointegrate Azure Active directory 감사 로그

1. Hello 명령 프롬프트를 열고이 명령을 실행 합니다.

   ``cd c:\Program Files\Microsoft Azure Log Integration``

2. 다음 명령을 실행합니다. 
 
   ``azlog createazureid``

   이 명령은 사용자에게 Azure 로그인을 요구합니다. hello 명령 후 Azure Active Directory 서비스 사용자를 만듭니다 hello Azure AD 테 넌 트에서 해당 호스트 hello는 hello 로그인 한 사용자가 관리자, 공동 관리자 또는 소유자는 Azure 구독. hello에 로그인 한 사용자가 게스트 사용자를 hello Azure AD 테 넌 트에만 hello 명령이 실패 합니다. 인증 tooAzure Azure AD를 통해 수행 됩니다. Azure 로그 통합에 대 한 서비스 사용자를 만들면 hello 액세스 tooread Azure 구독에서 지정 된 Azure AD id 만들어집니다.

3. 실행된 hello 다음 명령은 tooprovide 테 넌 트 ID Hello 테 넌 트 관리자 역할 toorun hello 명령 toobe 소속이 필요합니다.

   ``Azlog.exe authorizedirectoryreader tenantId``

   예제:

   ``AZLOG.exe authorizedirectoryreader ba2c0000-d24b-4f4e-92b1-48c4469999``

4. 여기에 따라 Azure Active Directory 감사 로그 JSON 파일 hello 폴더 tooconfirm hello 만들어집니다 확인 합니다.

   * **C:\Users\azlog\AzureActiveDirectoryJson**
   * **C:\Users\azlog\AzureActiveDirectoryJsonLD**

hello 다음 비디오에서는 보여줍니다이 문서에서 다루는 hello 단계:

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Azure-AD-Integration/player]


> [!NOTE]
> 보안 정보 및 이벤트 (SIEM) 관리 시스템으로 hello JSON 파일에서 hello 정보 보기에 대 한 자세한 내용은 SIEM 공급 업체에 문의 합니다.

커뮤니티 지원 hello를 통해 사용할 수는 [Azure 로그 통합 MSDN 포럼](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration)합니다. 이 포럼으로 수 있도록 hello Azure 로그 통합 커뮤니티 toosupport에 서로 관련 된 질문, 대답, 팁 및 요령 합니다. 또한 hello Azure 로그 통합 팀이이 포럼을 모니터링 하 고 가능 하기는 데 도움이 됩니다.

[지원 요청](../azure-supportability/how-to-create-azure-support-request.md)을 열 수도 있습니다. 선택 **로그 통합** hello 서비스 지원을 요청 합니다.

## <a name="next-steps"></a>다음 단계
Azure 로그 통합에 대해 자세히 toolearn 참조:

* [Azure 로그에 대한 Microsoft Azure 로그 통합](https://www.microsoft.com/download/details.aspx?id=53324): 이 다운로드 센터 페이지는 Azure 로그 통합에 대한 세부 정보, 시스템 요구 사항 및 설치 지침을 제공합니다.
* [로그 통합 소개 tooAzure](security-azure-log-integration-overview.md):이 문서에서는 소개 tooAzure 로그 통합의 주요 기능 및 작동 방식입니다.
* [구성 단계를 파트너](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/):이 블로그 게시물 표시 방법으로 Azure 로그 통합 toowork tooconfigure 파트너 솔루션 Splunk, HP ArcSight 및 IBM QRadar 합니다.
* [Azure 로그 통합 FAQ](security-azure-log-integration-faq.md): 이 문서는 Azure 로그 통합에 대한 질문에 답변합니다.
* [Azure 로그 통합 보안 센터 알림을 통합](../security-center/security-center-integrating-alerts-with-log-integration.md):이 문서에서는 Azure 진단 및 로그 분석을 사용 하 여 Azure 감사 로그에서 수집 하는 가상 컴퓨터 보안 이벤트와 함께 toosync 보안 센터 경고 방법 또는 SIEM 솔루션입니다.
* [Azure 진단 및 Azure에 대 한 새로운 기능 감사 로그](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/):이 블로그 게시물에서는 tooAzure 감사 로그 소개 하 고 Azure 리소스의 hello 작업을 파악할 수 있는 기타 기능입니다.
