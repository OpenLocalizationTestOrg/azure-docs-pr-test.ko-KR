---
title: "aaaAzure 서비스 패브릭 보안 모범 사례 | Microsoft Docs"
description: "이 문서에서는 Azure Service Fabric 보안을 위한 여러 모범 사례를 제공합니다."
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
ms.openlocfilehash: 483a21240da17d56bb4641653093ddcbad379d6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-security-best-practices"></a>Azure Service Fabric 보안 모범 사례
Azure에 응용 프로그램을 배포하는 것은 빠르고, 쉽고, 비용 효율적입니다. 프로덕션 유용한 toohave에 클라우드 응용 프로그램을 배포 하기 전에 응용 프로그램을 목록에 대 한 필수 및 권장 모범 사례를 평가할 때 tooassist는 것이 좋습니다.

Azure 서비스 패브릭은 분산된 시스템 플랫폼으로 쉽게 toopackage를 사용 하면을 배포 하 고 확장성과 안정성이 뛰어난 microservices 관리 합니다. 또한 서비스 패브릭 hello를 개발 및 클라우드 응용 프로그램 관리에서 중요 한 문제를 해결 합니다. 개발자와 관리자가 복잡한 인프라 문제를 피하고 업무 수행에 필수적인 까다로운 워크로드를 확장 가능하고 신뢰할 수 있으며 관리가 가능하도록 구현하는 데 집중할 수 있습니다. 

각 모범 사례에 대해 다음과 같이 설명합니다.

-   어떤 hello 것이 좋습니다.
-   이유는 tooenable 최선의 방법을
-   Tooenable hello에 대 한 모범 사례를 실패 한 경우 hello 결과 버릴
-   Tooenable hello에 대 한 최상의 정보를 어떻게 알 수 있습니다.

현재 Azure 서비스 패브릭 보안 최선의 구현 방법을 hello를 해야 합니다.

-   Azure 리소스 Manager(ARM) 템플릿과 toocreate 보안 클러스터 서비스 패브릭 Azure PowerShell 모듈을 사용 하 여
-   X.509 인증서 사용
-   보안 정책 구성
-   Reliable Actors 보안 구성
-   Azure Service Fabric에 대해 SSL 구성
-   Azure Service Fabric을 통한 네트워크 격리/보안
-   보안을 위해 Key Vault 설정
-   사용자가 tooroles 할당


## <a name="best-practices-for-securing-your-cluster"></a>클러스터를 보호하기 위한 모범 사례

**큰 그림**

항상 보안 클러스터 사용
-   클러스터 보안 - 인증서 사용
-   클라이언트 액세스(관리자 및 읽기 전용) – AAD 사용

자동 배포 사용
-   스크립트 toogenerate를 사용 하 여, 배포 하 고, 암호 롤오버
-   Hello 비밀 KV, 다른 모든 클라이언트 액세스를 위해 AD를 사용 하 여
-   사람의 인증 없이 액세스할 toothem이 있어야 합니다.

또한 hello 다음 사항을 고려 합니다.
-   네트워크 보안 그룹(NSG)을 사용하여 DMZ 만들기
-   클러스터를 클러스터 Vm 또는 toomanage 점프 서버 tooRDP 사용

클러스터에서 실행 되는 프로덕션 작업 되었을 경우, 특히 tooyour 클러스터를 연결 하지 못하도록 보안된 tooprevent 권한이 없는 사용자가 있어야 합니다. 가능한 toocreate 보안 되지 않은 클러스터는 아니지만를 통해 익명 사용자에 게 tooconnect tooit 관리 끝점 toohello를 노출 하는 경우 공용 인터넷 합니다.

기술 tooimplement 이러한 시나리오를 사용 합니다. hello [클러스터 보안 시나리오](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security) 됩니다.

-   노드 보안 This hello Vm 및 hello 클러스터의 컴퓨터 간의 통신을 보호합니다. 이렇게 하면 권한 있는 toojoin hello 클러스터 된 컴퓨터에만 응용 프로그램 및 hello 클러스터에서 서비스 호스팅에 참여할 수 있습니다.
Azure에서 실행되는 클러스터 또는 Windows에서 실행되는 독립 실행형 클러스터는 Windows Server 컴퓨터에 대한 [인증서 보안](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-x509-security) 또는 [Windows 보안](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-windows-security)을 사용할 수 있습니다.
-   클라이언트-노드 보안-본 서비스 패브릭 클라이언트와 hello 클러스터의 개별 노드 간의 통신을 보호합니다.
-   역할 기반 액세스 제어 (RBAC)-각각에 대해 별도 id (인증서, AAD 등)를 제공 하 여 hello 클러스터 생성 시 hello 관리자 및 사용자 클라이언트 역할 사용자 지정 합니다.
-   보안 권장 사항-Azure에 대 한 클러스터, 노드 보안을 위해 AAD tooauthenticate 클라이언트 보안 및 인증서를 사용 하는 것이 좋습니다.

tooconfigure hello 독립 실행형 Windows 클러스터 참조 [독립 실행형 windows 클러스터에 대 한 설정을 구성](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest)합니다.

서비스 패브릭 Azure PowerShell 모듈 toocreate 보안 클러스터 및 Azure 리소스 관리자 템플릿을 사용 합니다.
Azure Resource Manager를 사용하여 Azure에 보안 Azure Service Fabric 클러스터를 설정하는 단계를 안내하는 단계별 가이드는 [여기](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm)서 제공합니다.

클러스터 hello Azure 리소스 관리자 템플릿 toocustomize를 사용 합니다.
-   VM VHD에 대한 설치 관리 저장소

Hello Azure 리소스 관리자 템플릿 toodrive 변경 tooyour 리소스 그룹을 사용 하 여
-   간편한 구성 관리
-   감사

클러스터 구성을 코드로 처리
-   한 정보가 toodeploy 선택 hello 구성을 확인 하는 중
-   암시적 명령을 tootweak 리소스를 직접 사용 하지 마십시오

여러 가지 hello [서비스 패브릭 응용 프로그램 수명 주기](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-lifecycle) 자동화할 수 있습니다. [Service Fabric Azure PowerShell 모듈](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications#upload-the-application-package)은 Azure Service Fabric 응용 프로그램의 배포, 업그레이드, 제거 및 테스트를 위한 일반적인 작업을 자동화합니다. 앱 관리를 위한 관리되는 API 및 HTTP API도 사용 가능합니다.

## <a name="use-x509-certificates"></a>X.509 인증서 사용
항상 X.509 인증서 또는 Windows 보안을 사용하여 클러스터를 보호해야 합니다. 보안 클러스터를 만들 때에만 구성 하 고 hello 클러스터가 만들어진 후 가능한 tooenable 보안은 합니다.

지정 하는 경우는 [클러스터 인증서](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-x509-security), ClusterCredentialType tooX509의 hello 값을 설정 합니다. 외부 연결에 대 한 서버 인증서를 지정 하는 경우에 hello ServerCredentialType tooX509 설정 합니다.

-   프로덕션 워크로드를 실행하는 클러스터에 사용되는 인증서는 올바르게 구성된 Windows Server 인증서 서비스를 사용하여 만들어지거나 승인된 CA(인증 기관)에서 획득해야 합니다.
-   프로덕션 환경에서 MakeCert.exe와 같은 도구를 사용하여 만든 임시 또는 테스트 인증서를 사용하지 마세요.
-   자체 서명된 인증서를 사용할 수 있지만 프로덕션이 아닌 테스트 클러스터에 대해서만 이러한 인증서를 사용해야 합니다.

Hello 클러스터는 보안 되지 않습니다. 누구든지 익명으로 연결하고 관리 작업을 수행할 수 있으므로 프로덕션 클러스터가 항상 X.509 인증서 또는 Windows 보안을 사용하여 보호되어야 합니다.

서비스 패브릭 클러스터에 있는 tooenable 인증서 참조 하는 방법을 더 toolearn [더하거나 빼는 서비스 패브릭 클러스터에 대 한 인증서](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-update-certs-azure)합니다.

## <a name="configure-security-policies"></a>보안 정책 구성
서비스 패브릭 예를 들어 hello 사용자 계정-배포의 hello 시 응용 프로그램에서 사용 되는 보안 hello 리소스, 파일, 디렉터리 및 인증서에도 도움이 됩니다. 따라서 공유되는 호스티드 환경에서도 서로 더욱 안전하게 응용 프로그램을 실행할 수 있습니다.

-   Active Directory 도메인 그룹 또는 사용자를 사용 하 여: Active Directory 사용자 또는 그룹 계정에 대 한 hello 자격 증명으로 hello 서비스를 실행할 수 있습니다. 도메인 내의 Active Directory 온-프레미스이며 Azure Active Directory(Azure AD)를 사용하지 않습니다. 도메인 사용자 또는 그룹을 사용 하 여 권한을 부여 받은 기타 리소스 hello 도메인 (예: 파일 공유)에 액세스할 수 있습니다.

-   HTTP 및 HTTPS 끝점에 대 한 보안 액세스 정책을 할당: toothese 포트에 할당 되는 SecurityAccessPolicy tooensure를 지정 해야 RunAs 정책 tooa 서비스를 적용 하는 경우 hello HTTP 프로토콜을 사용 하 여 끝점 리소스를 선언 하는 hello 서비스 매니페스트 끝점은 올바르게 액세스 제어 hello hello 서비스가 실행 되는 실행 사용자 계정에 대해 나열 합니다. 그렇지 않은 경우 http.sys에 액세스 toohello 서비스 없고 hello 클라이언트에서 호출 에서도 오류를 받아야 합니다.
toolearn 서비스 패브릭 참조에 보안 정책을 더 사용 [응용 프로그램에 대 한 보안 정책을 구성](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-runas-security)합니다.

## <a name="reliable-actors-security-configuration"></a>Reliable Actors 보안 구성
서비스 패브릭 Reliable Actors는 hello 행위자 디자인 패턴을 구현 합니다. 모든 소프트웨어 디자인 패턴에서와 마찬가지로 소프트웨어 문제를 디자인 하는 여부에 따라 toouse 특정 패턴은 있도록 하는지 여부를 결정을 hello hello 패턴을 적합 합니다.

일반적인 지침으로 hello 행위자 패턴 toomodel 문제 또는 시나리오 경우 고려 합니다.
-   문제 영역은 1,000개 이상이라는 많은 수의 작고 독립적인 격리된 상태 및 논리 단위를 포함합니다.
-   Toowork 행위자의 상태를 쿼리 등의 외부 구성 요소에서 중요 한 상호 작용 하지 않아도 되는 단일 스레드 개체와 함께 사용 하는 것이 좋습니다.
-   행위자 인스턴스는 I/O 작업을 실행하여 예측할 수 없는 지연으로 호출자를 차단하지 않습니다.

서비스 패브릭 행위자 hello Reliable Actors 프레임 워크에서 구현 됩니다:는 행위자 패턴 기반 응용 프로그램 프레임 워크를 기반으로 구축 [서비스 패브릭 신뢰할 수 있는 서비스](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-introduction)합니다. 작성한 Reliable Actor 서비스는 각각 실제로 분할된 상태 저장 Reliable Service입니다.
동일한 toohello.NET 개체는 방식은.NET 형식의 인스턴스로 모든 행위자 행위자 형식의 인스턴스로 서 정의. 예를 들어 hello 기능 계산기를 구현 하는 행위자 형식 수 있으며 해당 형식의 다양 한 노드에서 클러스터를 통해 배포 되는 여러 작업자 있을 수 있습니다. 이러한 각 행위자는 행위자 ID에 의해 고유하게 식별됩니다.

[복제기 보안 구성](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-actors-kvsactorstateprovider-configuration) 복제 하는 동안 사용 되는 사용 되는 toosecure hello 통신 채널을 됩니다. 즉, 서비스 다른 사용자의 복제 트래픽을 인지 확인 하는 hello는 데이터에 항상 사용 가능한도 보안을 볼 수 없습니다. 기본적으로 빈 보안 구성 섹션에서는 복제 보안이 되지 않습니다.
복제기 구성 hello 행위자 상태 공급자 상태 안정성이 높아야 하는 일을 담당 하는 hello 복제기를 구성 합니다.

## <a name="configure-ssl-for-azure-service-fabric"></a>Azure Service Fabric에 대해 SSL 구성

서버 인증: [Authenticates](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) 알 수 있도록 hello 관리 클라이언트와 통신할 toohello 실제 클러스터에 클러스터 관리 끝점 tooa 관리 클라이언트 hello 합니다. 이 인증서도 제공 합니다.는 [SSL](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm) HTTPS 통해 서비스 패브릭 탐색기 및 hello HTTPS 관리 API에 대 한 합니다.
클러스터에 대한 사용자 지정 도메인 이름을 획득해야 합니다. CA에서 인증서를 요청할 때 hello 인증서의 주체 이름은 일치 해야 합니다 클러스터에 대해 사용 하는 hello 사용자 지정 도메인 이름.

응용 프로그램에 대 한 SSL을 tooconfigure, 먼저 tooget는 인증 기관 (CA)에서이 목적을 위해 인증서를 발급 하는 신뢰할 수 있는 타사 서명 된 SSL 인증서입니다. 이미 않아도 하나, 하는 경우 SSL 인증서를 판매 하는 회사에서 tooobtain 하나 해야 합니다.

hello 인증서 hello Azure에서 SSL 인증서에 대 한 요구 사항을 준수를 충족 해야 합니다.
-   hello 인증서 개인 키를 포함 해야 합니다.
-   키 교환, 내보낼 수 있는 tooa 개인 정보 교환 (.pfx) 파일에 대 한 hello 인증서를 만들어야 합니다.
-   hello 인증서의 주체 이름은 일치 해야 hello 사용 되는 도메인 tooaccess hello 클라우드 서비스입니다. Hello cloudapp.net 도메인에 대 한 인증 기관 (CA)에서 SSL 인증서를 가져올 수 없습니다. 사용자 지정 도메인 이름을 toouse 획득 해야 서비스에 액세스할 때. CA에서 인증서를 요청한 응용 프로그램 hello 인증서의 주체 이름은 hello 사용자 지정 도메인 이름 사용 tooaccess 일치 해야 합니다. 예를 들어 사용자 지정 도메인 이름이 contoso.com인 경우 CA에서 **.contoso.com** 또는 **www.contoso.com**에 대한 인증서를 요청합니다.
-   hello 인증서 최소 2048 비트 암호화를 사용 해야 합니다.

HTTP 안전 하지 않으며 주체 tooeavesdropping 공격 ¿¡´ hello hello 웹 브라우저 toohello 웹 서버 또는 다른 끝점 간에 전송 되는 데이터는 일반 텍스트로 전송 합니다. 즉 공격자가 신용카드 정보와 계정 로그인 같은 중요 데이터를 가로채 볼 수 있습니다. 데이터가 HTTPS를 사용하는 브라우저를 통해 전송 또는 게시될 경우 SSL이 그러한 정보를 암호화하여 가로채기로부터 보호합니다.

toolearn 더, 참조, [azure 응용 프로그램에 대 한 SSL 구성](https://docs.microsoft.com/azure/cloud-services/cloud-services-configure-ssl-certificate)합니다.

## <a name="network-isolationsecurity-with-azure-service-fabric"></a>Azure Service Fabric을 통한 네트워크 격리/보안
사용 하 여 [Azure 리소스 관리자 (ARM) 템플릿](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) 보안 클러스터 및 toocontrol hello 인바운드 및 아웃 바운드 네트워크 트래픽은 네트워크 보안 그룹을 사용 하 여 3 개의 노드 종류를 설정 하기 위한 샘플으로 합니다.

hello 템플릿 각 hello 가상 컴퓨터 크기 조정 set(VMSS) toocontrol hello 안팎 트래픽에 VMSS hello에 대 한 네트워크 보안 그룹에 있습니다. 기본적으로 hello 규칙 필요한 트래픽이 hello 모든 tooallow가 설정 hello 시스템 서비스 및 hello 응용 프로그램 포트 hello 서식 파일에 지정 합니다. 이러한 규칙을 검토 하 고 응용 프로그램에 대 한 새 작업을 비롯 한 요구 추가 변경 내용을 toofit를 확인 합니다.

자세한 내용은 [Azure Service Fabric – 일반적인 네트워킹 시나리오](https://docs.microsoft.com/azure/service-fabric/service-fabric-patterns-networking)를 참조하세요.

## <a name="set-up-a-key-vault-for-security"></a>보안을 위해 Key Vault 설정
인증서 서비스 패브릭 tooprovide toosecure 인증 및 암호화에에서 사용 되는 클러스터 및 해당 응용 프로그램의 다양 한 측면입니다.

서비스 패브릭 X.509 인증서 toosecure 클러스터를 사용 하 고 응용 프로그램 보안 기능을 제공 합니다. 키 자격 증명 모음을 너무 사용[인증서 관리](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-update-certs-azure) azure에서 서비스 패브릭 클러스터에 대 한 합니다. Azure에서 클러스터를 배포 하는 경우 서비스 패브릭 클러스터 만들기를 담당 하는 hello Azure 리소스 공급자에서 키 자격 증명 모음 인증서를 끌어온 hello 클러스터 Vm에 설치 합니다.

간의 관계를 hello [Azure 키 자격 증명 모음](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault), 즉 서비스 패브릭 클러스터 및 클러스터를 만들 때 주요 자격 증명 모음에 저장 된 인증서를 사용 하는 hello Azure 리소스 공급자입니다.

**리소스 그룹 만들기** hello 첫 번째 단계는 toocreate 주요 자격 증명 모음 용으로 특별히 리소스 그룹입니다. 리소스 그룹에 hello 주요 자격 증명 모음을 두는 것이 좋습니다. 이 작업에는 hello 계산 및 저장소 리소스 그룹이 포함 된 그룹 키 및 암호를 손실 하지 않고 서비스 패브릭 클러스터를 포함 하는 hello 리소스 그룹을 제거할 수 있습니다. 주요 자격 증명 모음을 포함 하는 hello 리소스 그룹 hello에 있어야 합니다. 사용 중인 hello 클러스터와 동일한 지역입니다.

**Hello 새 리소스 그룹에서 주요 자격 증명 모음 만들기** 배포 tooallow에서 계산 리소스 공급자 tooget 인증서 hello에 가상 컴퓨터 인스턴스 설치에 대 한 hello 키 자격 증명 모음을 사용할 수 있어야 합니다.
Azure 키 자격 증명 모음을 tooset 참조 하는 방법을 더 toolearn [Azure 키 자격 증명 모음 시작](https://docs.microsoft.com/azure/key-vault/key-vault-get-started)합니다.

## <a name="assign-users-roles"></a>사용자 역할 할당
Hello 응용 프로그램 toorepresent 클러스터를 만든 후 사용자가 서비스 패브릭에서 지 원하는 toohello 역할을 할당: 읽기 전용 및 관리자 Hello Azure 클래식 포털을 사용 하 여 hello 역할을 할당할 수 있습니다.

>[!Note]
> 서비스 패브릭의 역할에 대한 자세한 내용은 [서비스 패브릭 클라이언트의 역할 기반 액세스 제어](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-roles)를 참조하세요.

Azure 서비스 패브릭 연결된 tooa는 클라이언트에 대해 두 개의 서로 다른 액세스 제어 유형을 지원 [서비스 패브릭 클러스터](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm): 관리자와 사용자입니다. 액세스 제어 작업을 허용 hello 클러스터 관리자 toolimit 액세스 toocertain 클러스터 hello 클러스터를 보안 하는 사용자의 다른 그룹에 대 한 합니다.

## <a name="next-steps"></a>다음 단계
- Service Fabric [개발 환경](https://docs.microsoft.com/azure/service-fabric/service-fabric-get-started) 설정
- [Service Fabric 지원 옵션](https://docs.microsoft.com/azure/service-fabric/service-fabric-support)에 대해 알아봅니다.

