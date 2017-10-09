---
title: "작업 보안 검사 목록 aaaAzure | Microsoft Docs"
description: "이 문서에서는 Azure 운영 보안에 대한 일단의 검사 목록을 제공합니다."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: tomsh
ms.openlocfilehash: 03abe41ec828e929024ee59acd45b06410e9fbf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-operational-security-checklist"></a>Azure 운영 보안 검사 목록
Azure에 응용 프로그램을 배포하는 것이 빠르고, 쉽고, 비용 효율적입니다. Tooconsider 있습니다에 대 한 필수 및 권장 작업 보안 작업의 목록에 대해 응용 프로그램을 평가할 때 검사 목록 tooassist 프로덕션 유용한 toohave에 클라우드 응용 프로그램을 배포 하기 전에 합니다.

## <a name="introduction"></a>소개

Azure에 사용할 수 있는 toodeploy 응용 프로그램 인프라 서비스의 모음을 제공 합니다. Azure Operational 보안 toohello 서비스, 컨트롤 및 기능 사용 가능한 toousers 데이터, 응용 프로그램 및 Microsoft Azure에서 기타 자산을 보호 하기 위한 참조 합니다.

-   tooget hello 최대 혜택 hello 클라우드 플랫폼에서 Azure 서비스를 활용 하 고 hello 검사 목록에 따라 좋습니다.
-   시간 및 해당 응용 프로그램 시작 하기 전에 hello 운영 준비를 평가 하는 리소스를 투자 하는 조직 있을 보다 모르고 있는 사용자를 사용 하 여 훨씬 더 빠른 속도의 만족 합니다. 이 작업을 수행할 때 검사 목록에는 응용 프로그램이 일관 되 고 전체적으로 계산 되는 매우 유용한 메커니즘 tooensure 될 수 있습니다.
-   hello 수준의 operational 평가 hello 조직의 클라우드 완성도 수준 및 hello 응용 프로그램의 개발 단계, 가용성 요구 및 데이터 민감도 요구 사항에 따라 달라 집니다.

## <a name="checklist"></a>검사 목록

이 검사 목록은 toohelp 기업에서는 Azure에서 복잡 한 엔터프라이즈 응용 프로그램을 배포 하는 대로 다양 한 작업 보안 고려 사항에 검토 것입니다. 조직에 대 한 보안 클라우드 마이그레이션 및 작업 전략을 계획 하는 사용 되는 toohelp 수도 있습니다.

|검사 목록 범주| 설명|
| ------------ | -------- |
| [<br>보안 역할 및 액세스 제어](https://docs.microsoft.com/azure/security-center/security-center-planning-and-operations-guide)|<ul><li>사용 하 여 [역할 기반 액세스 제어 (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) tooprovide 사용자 고유의 특정 범위에서 tooassign 권한 toousers, 그룹 및 응용 프로그램을 사용 합니다.</li></ul> |
| [<br>데이터 수집 및 저장](https://docs.microsoft.com/azure/storage/storage-security-guide)|<ul><li>사용 하 여 저장소 계정 관리 평면 보안 toosecure 사용 하 여 [역할 기반 액세스 제어 (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure)합니다.</li><li>데이터 평면 보안 tooSecuring tooyour 데이터 사용 하 여 액세스 [공유 액세스 서명 (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) 및 액세스 정책을 저장 합니다.</li><li>HTTPS를 사용 하 여 전송 수준 암호화 –를 사용 하 고 암호화가 사용 하 여 hello [SMB (서버 메시지 블록 프로토콜) 3.0](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx) 에 대 한 [Azure 파일 공유](https://docs.microsoft.com/azure/storage/storage-dotnet-how-to-use-files)합니다.</li><li>사용 하 여 [클라이언트 쪽 암호화](https://docs.microsoft.com/azure/storage/storage-client-side-encryption) toostorage 보내는 toosecure 데이터 암호화 키를 단독으로 제어 해야 하는 경우 계정. </li><li>사용 하 여 [저장소 서비스 암호화 (SSE)](https://docs.microsoft.com/azure/storage/storage-service-encryption) tooautomatically Azure 저장소의 데이터를 암호화 하 고 [Azure 디스크 암호화](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) hello OS 및 데이터 디스크에 대 한 tooencrypt 가상 컴퓨터 디스크 파일입니다.</li><li>Azure를 사용 하 여 [Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/storage-analytics) toomonitor 권한 부여 입력; 같은 Blob 저장소와 사용자가 공유 액세스 서명 사용 또는 저장소 계정 키를 hello 경우 확인할 수 있습니다.</li><li>사용 하 여 [크로스-원본 자원 공유 (CORS)](https://docs.microsoft.com/rest/api/storageservices/cross-origin-resource-sharing--cors--support-for-the-azure-storage-services) 서로 다른 도메인에서 tooaccess 저장소 리소스입니다.</li></ul> |
|[<br>보안 정책 및 권장 사항](https://docs.microsoft.com/azure/security-center/security-center-planning-and-operations-guide)|<ul><li>사용 하 여 [Azure 보안 센터](https://docs.microsoft.com/azure/security-center/security-center-install-endpoint-protection) toodeploy 끝점 솔루션입니다.</li><li>추가 [웹 응용 프로그램 방화벽 (WAF)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) toosecure 웹 응용 프로그램입니다.</li><li>  사용 하 여 한 [다음 세대 방화벽 (NGFW)](https://docs.microsoft.com/azure/security-center/security-center-add-next-generation-firewall) Microsoft에서 파트너 tooincrease 보안 보호 합니다. </li><li>Azure 구독에 대 한 보안 연락처 세부 정보를 적용 합니다. 이 hello [Microsoft 보안 대응 센터 (MSRC)](https://technet.microsoft.com/security/dn528958.aspx) 발견 된 불법 또는 무단 당사자가 고객 데이터에 액세스 하는 경우이 연결 합니다.</li></ul> |
| [<br>ID 및 액세스 관리](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices)|<ul><li>[Azure AD를 사용하여 온-프레미스 디렉터리를 클라우드 디렉터리와 동기화합니다](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).</li><li>사용 하 여 [Single Sign On](https://azure.microsoft.com/resources/videos/overview-of-single-sign-on/) tooenable 사용자 tooaccess 자신의 조직 계정을 Azure AD의 기반으로 SaaS 응용 프로그램입니다.</li><li>사용 하 여 hello [암호 재설정 등록 활동](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-get-insights) 등록 하는 보고서 toomonitor hello 사용자입니다.</li><li>사용자에 대한 [MFA(Multi-Factor Authentication)](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication)를 사용하도록 설정합니다.</li><li>앱에 대 한 toouse 보안 id 기능을 개발자와 같은 [Microsoft SDL Security Development Lifecycle ()](https://www.microsoft.com/download/details.aspx?id=12379)합니다.</li><li>Azure AD Premium 비정상 보고서 및 [Azure AD ID 보호 기능](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection)을 사용하여 의심스러운 활동을 적극적으로 모니터링합니다.</li></ul> |
|[<br>지속적인 보안 모니터링](https://docs.microsoft.com/azure/security-center/security-center-planning-and-operations-guide)|<ul><li>맬웨어 평가 솔루션을 사용 하 여 [로그 분석](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) tooreport hello 인프라의 맬웨어 방지 보호 상태에 있습니다.</li><li>사용 하 여 [평가 업데이트](https://docs.microsoft.com/azure/operations-management-suite/oms-solution-update-management) toodetermine hello 전체 노출을 toopotential 보안 문제를 여부와 사용자 환경에 대 한 이러한 업데이트는 중요도 또는 합니다.</li><li>hello [Id 및 액세스](https://docs.microsoft.com/azure/operations-management-suite/oms-security-monitoring-resources) 사용자의 개요를 제공 </li><ul><li>사용자 ID 상태</li><li>, 실패 한 시도 toolog 개수</li><li>  hello 아웃 잠겨진 계정의 재전송 시도 하는 동안 사용 된 사용자 계정</li> <li>암호가 변경되거나 다시 설정된 계정 </li><li>현재 로그인한 계정 수</li></ul></ul> |
| [<br>Azure Security Center 검색 기능](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities)|<ul><li>사용 하 여 [검색 기능이](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities), tooidentify 활성 위협이 Microsoft Azure 리소스를 대상으로 지정 합니다.</li><li>사용 하 여 [위협 인텔리전스 통합](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/19/get-threat-intelligence-reports-with-azure-security-center/) 알려진된 믿지 못할 자 글로벌를 활용 하 여 위협 인텔리전스 Microsoft 제품 및 서비스에서 hello에 대 한 좋아보이지 [Microsoft Digital Crimes 단위 (DCU)](https://www.microsoft.com/stories/cyber.aspx), hello [Microsoft 보안 대응 센터 (MSRC)](https://docs.microsoft.com/azure/security/azure-security-response-center), 및 외부 피드입니다.</li><li>사용 하 여 [동작 분석](https://blogs.technet.microsoft.com/enterprisemobility/2016/06/30/ata-behavior-analysis-monitoring/) 알려진된 패턴 toodiscover 악의적인 동작을 적용 하는 합니다. </li><li>사용 하 여 [이상 탐지](https://msdn.microsoft.com/library/azure/dn913096.aspx) 통계 프로 파일링 toobuild 기록 초기 계획을 사용 하 여 합니다.</li></ul> |
| [<br>DevOps(개발자 작업)](https://docs.microsoft.com/azure/architecture/checklist/dev-ops)|<ul><li>[인프라 (IaC) 코드로](https://azure.microsoft.com/documentation/articles/resource-group-authoring-templates/) 이 hello 자동화 및 만들기의 유효성을 검사 하 고 안전 하 고 안정적인 응용 프로그램 호스팅 플랫폼을 제공 toohelp 네트워크 및 가상 컴퓨터 종료를 사용 하면 좋습니다.</li><li>[연속 통합 및 배포](https://www.visualstudio.com/docs/build/overview) 드라이브 hello 진행 중인 병합 하 고 초기 toofinding 결함을 유발 하는 코드를 테스트 합니다. </li><li>[Release Management](https://msdn.microsoft.com/library/vs/alm/release/overview)는 파이프라인의 각 단계를 통해 자동화된 배포를 관리합니다.</li><li>응용 프로그램 상태뿐만 아니라 고객 사용을 위한 프로덕션 환경을 포함하여 실행 중인 응용 프로그램의 [앱 성능 모니터링](https://azure.microsoft.com/documentation/articles/app-insights-start-monitoring-app-health-usage/)을 사용하면 조직에서 가설을 세우고 전략을 신속하게 유효성을 검사하거나 반증할 수 있습니다.</li><li>사용 하 여 [부하 테스트 및 자동 크기 조정](https://www.visualstudio.com/docs/test/performance-testing/getting-started/getting-started-with-performance-testing) 앱 tooimprove 배포 품질 toomake 앱 항상는 사용할 수 없거나 최신 toocater toohello 비즈니스 요구에 성능 문제를 확인할 수 있습니다.</li></ul> |


## <a name="conclusion"></a>결론
많은 조직에서 Azure에 클라우드 응용 프로그램을 성공적으로 배포하고 운영했습니다. hello 검사 목록을 제공 해야 하는 여러 가지 검사 목록의 강조 표시 도와 tooincrease hello 가능성 성공적인 배포과 불만 없는 작업. Azure에서는 기존 및 새 응용 프로그램 배포에 대한 이러한 운영 및 전략적 고려 사항을 적용하는 것이 좋습니다.

## <a name="next-steps"></a>다음 단계
이 문서에 도입 된 보안 및 감사 솔루션 tooOMS 있었습니다. OMS 보안에 대해 자세히 toolearn hello 다음 문서 참조:

- [OMS(Operations Management Suite) 개요](https://docs.microsoft.com/en-us/azure/operations-management-suite/operations-management-suite-overview)
- [설계 및 운영 보안(영문)](https://www.microsoft.com/trustcenter/security/designopsecurity)
- [Azure Security Center 계획 및 작업](https://docs.microsoft.com/azure/security-center/security-center-planning-and-operations-guide)
