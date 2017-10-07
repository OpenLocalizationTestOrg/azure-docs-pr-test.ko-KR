---
title: "aaaAzure 서비스 패브릭 보안 개요 | Microsoft Docs"
description: "이 문서는 Azure 서비스 패브릭 보안 hello에 대 한 개요를 제공합니다."
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
ms.date: 08/04/2017
ms.author: tomsh
ms.openlocfilehash: ec5355983c5d59f4e0c3b855965f03ac47f1a4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-security-overview"></a>Azure Service Fabric 보안 개요
[Azure 서비스 패브릭](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview) 는 분산된 시스템 플랫폼으로 쉽게 toopackage를 사용 하면을 배포 하 고 확장 가능 하 고 안정적인 마이크로 서비스를 관리 합니다. 서비스 패브릭 hello를 개발 및 클라우드 응용 프로그램 관리에서 중요 한 문제를 해결 합니다. 개발자와 관리자가 복잡한 인프라 문제를 피하고 업무 수행에 필수적인 까다로운 워크로드를 확장 가능하고 신뢰할 수 있으며 관리가 가능하도록 구현하는 데 집중할 수 있습니다.

이 Azure 서비스 패브릭 보안 개요 문서 hello 영역을 다음에 중점을 둡니다.

-   클러스터 보안 설정
-   모니터링 및 진단
-   인증서를 사용한 보안
-   RBAC(역할 기반 액세스 제어)
-   Windows 보안을 사용한 클러스터 보안
-   Service Fabric에서 응용 프로그램 보안 구성
-   Azure Service Fabric 보안에서 서비스에 대한 통신 보호 

## <a name="securing-your-cluster"></a>클러스터 보안 설정
Azure 서비스 패브릭은 컴퓨터의 클러스터에서 서비스는 orchestrator, 클러스터에서 실행 되는 프로덕션 작업 되었을 경우, 특히 tooyour 클러스터를 연결 하지 못하도록 보안된 tooprevent 권한이 없는 사용자가 있어야 합니다. 가능한 toocreate 보안 되지 않은 클러스터는 아니지만를 통해 익명 사용자에 게 tooconnect tooit 관리 끝점 toohello를 노출 하는 경우 공용 인터넷 합니다.

이 섹션 독립 실행형 또는 Azure에서 실행 중인 클러스터에 대 한 보안 시나리오의 hello 개요를 제공 하 고 사용 되는 기술 tooimplement 다양 한 시나리오 hello 합니다. hello 클러스터 보안 시나리오입니다.

-   노드 간 보안
-   클라이언트-노드 보안

### <a name="node-to-node-security"></a>노드 간 보안
Hello Vm 또는 hello 클러스터의 컴퓨터 간의 통신을 보호합니다. 이렇게 하면 권한 있는 toojoin hello 클러스터 된 컴퓨터에만 응용 프로그램 및 hello 클러스터에서 서비스 호스팅에 참여할 수 있습니다.

Azure에서 실행되는 클러스터 또는 Windows에서 실행되는 독립 실행형 클러스터는 Windows Server 컴퓨터에 대한 [인증서 보안](https://msdn.microsoft.com/library/ff649801.aspx) 또는 [Windows 보안](https://msdn.microsoft.com/library/ff649396.aspx)을 사용할 수 있습니다.

**노드 간 인증서 보안**

서비스 패브릭 클러스터를 만들 때 hello 노드 유형 구성의 일부로 지정 하는 X.509 서버 인증서를 사용 합니다. 증서 정보 및 [인증서 획득 또는 생성 방법](https://docs.microsoft.com/dotnet/framework/wcf/feature-details/working-with-certificates)에 대한 빠른 개요는 이 문서에서 제공됩니다.

인증서 보안 hello Azure 포털을 통해, Azure 리소스 관리자 템플릿 또는 독립 실행형 JSON 템플릿을 hello 클러스터를 만드는 동안 구성 됩니다. 기본 인증서 및 인증서 롤오버에 사용되는 선택적 보조 인증서를 지정할 수 있습니다. hello 지정 하는 기본 및 보조 인증서 계정과 달라 야 hello 관리 클라이언트와 읽기 전용 클라이언트 인증서에 대해 지정한 [클라이언트 노드 보안](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security)합니다.

### <a name="client-to-node-security"></a>클라이언트-노드 보안
클라이언트 toonode 보안이 클라이언트 Id를 사용 하 여 구성 됩니다. 클라이언트와 hello 클러스터 간 트러스트 tooestablish는 hello 클러스터 tooknow 신뢰할 수 있는 클라이언트 id를 구성 해야 합니다. 이 작업은 두 가지 방법으로 수행할 수 있습니다.

-   연결할 수 있는 hello 도메인 그룹 사용자 지정 또는
-   연결할 수 있는 hello 도메인 노드 사용자 지정 합니다.

서비스 패브릭 연결된 tooa 서비스 패브릭 클러스터에 있는 클라이언트에 대 한 두 개의 서로 다른 액세스 제어 종류를 지원 합니다.

-   관리자
-   사용자

액세스 제어는 클러스터 관리자 toolimit 액세스 toocertain 유형의 클러스터 작업이 서로 다른 hello 클러스터를 보안 하는 사용자, 그룹에 대 한 hello에 대 한 hello 기능을 제공 합니다. 관리자에 대 한 모든 권한을 toomanagement 기능 (읽기/쓰기 기능만 포함)가 있습니다. 사용자가 기본적으로 읽기 액세스 toomanagement 기능 (예: 쿼리 기능) 및 hello 기능 tooresolve 응용 프로그램 및 서비스입니다.

**클라이언트-노드 인증서 보안**

리소스 관리자 템플릿 또는 관리 클라이언트 인증서 및/또는 사용자 클라이언트 인증서를 지정 하 여 독립 실행형 JSON 템플릿 hello Azure 포털을 통해 hello 클러스터를 만드는 동안 클라이언트 노드 인증서 보안이 구성 됩니다. hello 관리 클라이언트와 사용자 클라이언트 인증서 지정 hello 기본 및 보조 인증서 노드를 보안에 대해 지정한 계정과 달라 야 합니다.

Hello 관리 인증서를 사용 하 여 toohello 클러스터를 연결 하는 클라이언트에 대 한 모든 권한을 toomanagement 기능이. Hello 읽기 전용 사용자 클라이언트 인증서를 사용 하 여 toohello 클러스터를 연결 하는 클라이언트 기능이 읽기 권한을 toomanagement. 이러한 인증서 hello에 사용 되며 다른 단어에서 역할 기반 액세스 제어를 (RBAC)를 만듭니다.

Azure 읽을 [Azure 리소스 관리자 템플릿을 사용 하 여 클러스터를 설정](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) toolearn tooconfigure 클러스터에서 보안 인증서 하는 방법입니다.

**Azure에서 클라이언트-노드 AAD(Azure Active Directory) 보안**

Azure에서 실행 하는 클러스터 액세스 Azure Active Directory (AAD)를 사용 하 여 toohello 관리 끝점 보안 수도 있습니다. 참조 [Azure 리소스 관리자 템플릿을 사용 하 여 클러스터를 설정](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) toocreate 필요한 AAD 아티팩트 hello 하는 방법에 대 한 내용은 어떻게 toopopulate 시 이러한 클러스터 만들기 및 tooconnect toothose 나중에 클러스터입니다.

AAD에 웹 기반 로그인 UI로 응용 프로그램 및 응용 프로그램은 네이티브 클라이언트 환경을으로 분할 되는 조직 (테 넌 트로 알려짐) toomanage 사용자 액세스 tooapplications를 수 있습니다.

서비스 패브릭 클러스터 여러 항목 지점 tooits 관리 기능을 제공 웹 기반 서비스 패브릭 탐색기 및 Visual Studio hello 포함 합니다. 결과적으로, toocontrol 액세스 toohello 클러스터에 대 한 두 개의 AAD 응용 프로그램, 웹 응용 프로그램 및 한 네이티브 응용 프로그램을 만듭니다.
Azure의 클러스터에 대 한 노드를 보안에 대 한 AAD tooauthenticate 클라이언트 보안 및 인증서를 사용 것이 좋습니다.

독립 실행형 Windows Server 클러스터의 경우 Windows Server 2012 R2 및 Active Directory가 있는 경우 GMA(그룹 관리 계정)로 Windows 보안을 사용하는 것이 좋습니다. 그렇지 않은 경우 여전히 Windows 계정으로 Windows 보안을 사용합니다.

## <a name="monitoring-and-diagnostics-for-azure-service-fabric"></a>Azure Service Fabric 모니터링 및 진단
[모니터링 및 진단](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-overview) 중요 toodeveloping, 테스트 및 응용 프로그램 및 서비스 모든 환경에 배포 됩니다. Service Fabric 솔루션은 로컬 개발 환경 또는 프로덕션 환경에서 응용 프로그램과 서비스가 예상대로 작동하는지 확인하는 데 도움이 되는 모니터링 및 진단을 계획하고 구현할 때 가장 효과적입니다.

보안 관점에서 모니터링의 주요 목표 hello 및 진단에:

-   검색 하 고 보안 이벤트 tooa 인해 수 있는 하드웨어 및 인프라 문제를 진단 합니다.
-   손상의 지표(IoC)를 제공할 수 있는 소프트웨어와 앱 문제를 검색합니다.
-   리소스를 이해 소비 toohelp 부주의 한 서비스 거부를 방지 합니다.

모니터링의 전체 워크플로 hello 및 진단 세 단계로 구성 됩니다.

-   **이벤트 생성:** 여기에 이벤트 (로그, 추적, 사용자 지정 이벤트) hello 인프라 (클러스터) 및 응용 프로그램 / 서비스 수준 모두에 있습니다. 에 대해 자세히 알아보세요 [인프라 수준 이벤트](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-generation-infra) 및 [응용 프로그램 수준 이벤트](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-generation-app) tooadd 계측을 추가 하는 방법 및 toounderstand 제공 하는 것입니다.
-   **이벤트 집계:** 생성 된 이벤트 수집 및 집계 표시 하려면 먼저 toobe 필요 합니다. 일반적으로 사용할 수 있는 권장 [Azure 진단](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-aggregation-wad) (유사한 tooagent 기반 로그 수집) 또는 [EventFlow](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow) (in process 로그 컬렉션).
-   **분석:** 이벤트 필요 toobe 시각화 된 있고 일부 형식, tooallow에 액세스할 수 있는 분석 및 필요에 따라 표시 합니다. 모니터링 및 진단 데이터의 toohello 분석 및 시각화 있어 hello 시장에 존재 하는 몇 가지 훌륭한 플랫폼 가지가 있습니다. hello 두 가지 권장 되는 [OMS](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-analysis-oms) 및 [Application Insights](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-analysis-appinsights) tootheir와의 통합 서비스 패브릭 때문입니다.

사용할 수도 있습니다 [Azure 모니터](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) toomonitor 서비스 패브릭 클러스터 기반이 되는 Azure 리소스를 hello 다양 합니다.

그런 다음 안정성은는 별도 서비스 상태를 관찰할 수 있으며 서비스 및 보고서 상태 간에 부하를 hello 상태 모델 계층 구조에서 모든 항목입니다. 이 단일 서비스의 hello 보기를 기준으로 검색 되지 않는 오류를 방지할 수 있습니다. Watchdogs (예: 저장소에서 로그 파일을 정리 하는 특정 시간 간격) 사용자 상호 작용 없이 수정 작업을 수행 하는 것이 좋습니다 toohost 코드도 있습니다. [여기](https://azure.microsoft.com/resources/samples/service-fabric-watchdog-service/)에서 샘플 watchdog 서비스 구현을 찾을 수 있습니다.

## <a name="secure-using-certificates"></a>인증서를 사용한 보안
인증서를 사용 하 여 어떻게 간의 toosecure hello 통신 hello 독립 실행형 Windows 클러스터의 다양 한 노드는 방법과 tooauthenticate 연결 하는 클라이언트 toothis 클러스터 X.509 인증서를 사용 하 여 표시 합니다. 이렇게 하는 권한이 있는 사용자는 hello 클러스터를 액세스할 수 있습니다 hello 배포 된 응용 프로그램 관리 작업을 수행 합니다. Hello 클러스터가 생성 될 때 hello 클러스터에 대 한 인증서 보안을 설정 해야 합니다.

### <a name="x509-certificates-and-service-fabric"></a>X.509 인증서 및 서비스 패브릭
X.509 디지털 인증서는 자주 사용 되는 tooauthenticate 클라이언트 및 서버와 tooencrypt와 메시지에 디지털 서명 합니다.

hello 다음 표에 클러스터 설치에서 필요한 hello 인증서.

|인증서 정보 설정 |설명|
|-------------------------------|-----------|
|ClusterCertificate|    이 인증서는 hello 노드 클러스터 간의 필요한 toosecure hello 통신입니다. 업그레이드에 두 개의 다른 인증서, 기본 및 보조 인증서를 사용할 수 있습니다.|
|ServerCertificate| 이 인증서는 tooconnect toothis 클러스터를 읽으려고 할 때 toohello 클라이언트를 표시 됩니다. 업그레이드에 두 개의 다른 서버 인증서, 기본 및 보조 인증서를 사용할 수 있습니다.|
|ClientCertificateThumbprints|  Tooinstall hello 인증 클라이언트에서 인증서의 집합입니다.|
|ClientCertificateCommonNames|  CertificateCommonName hello에 대 한 hello 첫 번째 클라이언트 인증서의 hello 일반 이름을 설정 합니다. hello CertificateIssuerThumbprint이이 인증서의 발급자 hello에 대 한 hello 지문입니다.|
|ReverseProxyCertificate|   이것은 사용할 수 있는 선택적 인증서는 toosecure 하려는 경우 지정 된 프로그램 [역방향 프록시](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy)합니다.|

인증서 보호에 대한 자세한 내용은 [여기를 클릭](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-x509-security)합니다.

## <a name="role-based-access-control-rbac"></a>RBAC(역할 기반 액세스 제어)
액세스 제어 작업을 허용 hello 클러스터 관리자 toolimit 액세스 toocertain 클러스터 hello 클러스터를 보안 하는 사용자의 다른 그룹에 대 한 합니다. Tooa 클러스터를 연결 하는 클라이언트에는 두 개의 서로 다른 액세스 제어 형식을 사용할: 관리자 역할 및 사용자 역할입니다.

관리자에 대 한 모든 권한을 toomanagement 기능 (읽기/쓰기 기능만 포함)가 있습니다. 사용자가 기본적으로 읽기 액세스 toomanagement 기능 (예: 쿼리 기능) 및 hello 기능 tooresolve 응용 프로그램 및 서비스입니다.

Hello 관리자 및 사용자 클라이언트 역할 타임 시 지정한 hello 클러스터 생성의 별도 id (인증서, AAD 등)를 제공 하 여 각각에 대 한 합니다. Hello 기본 액세스 제어 설정 및 toochange 기본 설정을 hello 하는 방법에 대 한 자세한 내용은 참조 하십시오. [서비스 패브릭 클라이언트에 대 한 역할 기반 액세스 제어](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-roles)합니다.

## <a name="secure-standalone-cluster-using-windows-security"></a>Windows 보안을 사용하여 독립 실행형 클러스터 보안
tooprevent 무단 액세스 tooa 서비스 패브릭 클러스터, hello 클러스터를 보호 해야 합니다. 보안은 hello 클러스터 프로덕션 워크 로드를 실행 하는 경우에 특히 중요 합니다. Windows 보안을 사용 하 여 tooconfigure 노드와 노드 및 노드 클라이언트 보안 ClusterConfig.JSON 파일 hello 하는 방법을 설명 합니다.

**gMSA를 사용하여 Windows 보안 구성**

노드 toonode 보안을 설정 하 여 구성한 [ClustergMSAIdentity](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-windows-security) 서비스 패브릭 toorun gMSA에서 필요로 하는 경우. 노드 간 순서 toobuild 트러스트 관계에 있도록 해야 서로 인식 합니다.

클라이언트 toonode 보안이 ClientIdentities를 사용 하 여 구성 됩니다. 클라이언트와 hello 클러스터 간의 순서 tooestablish 신뢰 hello 클러스터 tooknow 신뢰할 수 있는 클라이언트 id를 구성 해야 합니다.

**컴퓨터 그룹을 사용하여 Windows 보안 구성**

노드 toonode 보안이 toouse Active Directory 도메인 내에서 컴퓨터 그룹을 원하는 경우 ClusterIdentity를 사용 하 여 설정에 따라 구성 됩니다. 자세한 내용은 [Active Directory에 컴퓨터 그룹 만들기](https://msdn.microsoft.com/library/aa545347)를 참조하세요.

클라이언트-노드 보안은 클라이언트 ID를 사용하여 구성됩니다. 클라이언트와 hello 클러스터 간 트러스트 tooestablish는 hello 클러스터 tooknow hello 클라이언트를 신뢰할 수 있는 클러스터 hello 하는 id를 구성 해야 합니다. 다음 두 가지 방법으로 트러스트를 설정할 수 있습니다.

-   연결할 수 있는 hello 도메인 그룹 사용자가 지정 합니다.
-   연결할 수 있는 hello 도메인 노드 사용자 지정 합니다.

## <a name="configure-application-security-in-service-fabric"></a>Service Fabric에서 응용 프로그램 보안 구성
### <a name="managing-secrets-in-service-fabric-applications"></a>서비스 패브릭 응용 프로그램의 비밀 관리
이 메서드는 Service Fabric 응용 프로그램에서의 암호 관리에 도움이 됩니다. 저장소 연결 문자열, 암호, 일반 텍스트로 처리하면 안 되는 값 등 모든 민감한 정보를 비밀로 처리할 수 있습니다.

이 방법을 사용 하 여 [Azure 키 자격 증명 모음](https://docs.microsoft.com/azure/key-vault/key-vault-whatis) toomanage 키 및 암호. 그러나 암호를 사용 하 여 응용 프로그램에서 아무 곳 이나 호스트 클라우드 플랫폼 제약 없는 tooallow 응용 프로그램 배포 toobe tooa 클러스터입니다. 이 흐름은 주요 네 단계로 구성됩니다.

-   데이터 암호화 인증서를 가져옵니다.
-   클러스터의 hello 인증서를 설치 합니다.
-   Hello 인증서로 응용 프로그램을 배포 하는 경우 비밀 값을 암호화 하 고 서비스의 Settings.xml 구성 파일에 삽입 합니다.
-   읽기 암호화 된 암호 해독 하 여 Settings.xml 값 hello 동일한 암호화 인증서입니다.

>[!Note]
>[Service Fabric 응용 프로그램의 암호 관리](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-secret-management)에 대해 자세히 알아보세요.

### <a name="configure-security-policies-for-your-application"></a>응용 프로그램에 대한 보안 정책 구성
Azure 서비스 패브릭 보안을 사용 하 여 다른 사용자 계정으로 hello 클러스터에서 실행 되는 보안 응용 프로그램을 도울 수 있습니다. 서비스 패브릭 보안 예를 들어 hello 사용자 계정-배포의 hello 시 응용 프로그램에서 사용 되는 보안 hello 리소스, 파일, 디렉터리 및 인증서에도 도움이 됩니다. 따라서 공유되는 호스티드 환경에서도 서로 더욱 안전하게 응용 프로그램을 실행할 수 있습니다.
hello 단계는 다음과 같습니다.

-   서비스 설치 진입점에 대 한 hello 정책을 구성 합니다.
-   설치 진입점에서 PowerShell 명령 시작
-   로컬 디버깅에 대한 콘솔 리디렉션 사용
-   서비스 코드 패키지에 대한 정책 구성
-   HTTP 및 HTTPS 끝점에 보안 액세스 정책 할당

## <a name="secure-communication-for-services-in-azure-service-fabric-security"></a>Azure Service Fabric 보안에서 서비스에 대한 통신 보호 
보안 통신의 hello 가장 중요 한 측면 중 하나입니다. hello 신뢰할 수 있는 서비스 응용 프로그램 프레임 워크는 몇 가지 미리 작성 된 통신 스택 및 사용 되는 tooimprove 보안 일 수 있는 도구를 제공 합니다.

-   [서비스 원격 기능을 사용하는 경우 서비스 보호 도움말](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-secure-communication)
-   [WCF 기반 통신 스택을 사용하는 경우 서비스 보호 방법](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-secure-communication#help-secure-a-service-when-youre-using-a-wcf-based-communication-stack)

## <a name="next-steps"></a>다음 단계
- 클러스터 보안에 대한 개념 정보는 [Resource Manager 템플릿을 사용하여 Azure에 클러스터 만들기](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) 및 [Azure Portal](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-portal)을 참조하세요.
- 자세한 내용은 [Service Fabric 클러스터 보안](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security)을 참조하세요.
