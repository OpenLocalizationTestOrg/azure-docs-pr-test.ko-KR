---
title: "서비스 패브릭 클러스터 aaaSecure | Microsoft Docs"
description: "이러한 시나리오에 대 한 서비스 패브릭 클러스터와 hello 사용 되는 다른 기술 tooimplement hello 보안 시나리오를 설명합니다."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 26b58724-6a43-4f20-b965-2da3f086cf8a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: chackdan
ms.openlocfilehash: 249a9e85b8fbe174e2accee85a94d95b2872a3af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-cluster-security-scenarios"></a>서비스 패브릭 클러스터 보안 시나리오
서비스 패브릭 클러스터는 사용자가 소유하는 리소스입니다. 클러스터에서 실행 되는 프로덕션 작업 되었을 경우, 특히 tooyour 클러스터를 연결 하지 못하도록 보안된 tooprevent 권한이 없는 사용자가 있어야 합니다. 가능한 toocreate 보안 되지 않은 클러스터는 아니지만를 통해 익명 사용자에 게 tooconnect tooit 관리 끝점 toohello를 노출 하는 경우 공용 인터넷 합니다. 

이 문서는 독립 실행형 또는 Azure에서 실행 중인 클러스터에 대 한 보안 시나리오의 hello 개요를 제공 하 고 hello 사용 되는 기술 tooimplement 다양 한 시나리오. hello 클러스터 보안 시나리오입니다.

* 노드 간 보안
* 클라이언트-노드 보안
* RBAC(역할 기반 액세스 제어)

## <a name="node-to-node-security"></a>노드 간 보안
Hello Vm 또는 hello 클러스터의 컴퓨터 간의 통신을 보호합니다. 이렇게 하면 권한 있는 toojoin hello 클러스터 된 컴퓨터에만 응용 프로그램 및 hello 클러스터에서 서비스 호스팅에 참여할 수 있습니다.

![노드-노드 통신의 다이어그램][Node-to-Node]

Azure에서 실행되는 클러스터 또는 Windows에서 실행되는 독립 실행형 클러스터는 Windows Server 컴퓨터에 대한 [인증서 보안](https://msdn.microsoft.com/library/ff649801.aspx) 또는 [Windows 보안](https://msdn.microsoft.com/library/ff649396.aspx)을 사용할 수 있습니다.

### <a name="node-to-node-certificate-security"></a>노드 간 인증서 보안
서비스 패브릭 클러스터를 만들 때 hello 노드 유형 구성의 일부로 지정 하는 X.509 서버 인증서를 사용 합니다. 획득 하거나 만들어서 하는 방법 및 이러한 인증서의는 간략 한 개요는 hello이이 문서의 뒷부분에서 제공 됩니다.

인증서 보안 hello Azure 포털을 통해, Azure 리소스 관리자 템플릿 또는 독립 실행형 JSON 템플릿을 hello 클러스터를 만드는 동안 구성 됩니다. 기본 인증서 및 인증서 롤오버에 사용되는 선택적 보조 인증서를 지정할 수 있습니다. hello 지정 하는 기본 및 보조 인증서 계정과 달라 야 hello 관리 클라이언트와 읽기 전용 클라이언트 인증서에 대해 지정한 [클라이언트 노드 보안](#client-to-node-security)합니다.

Azure 읽을 [Azure 리소스 관리자 템플릿을 사용 하 여 클러스터를 설정](service-fabric-cluster-creation-via-arm.md) toolearn tooconfigure 클러스터에서 보안 인증서 하는 방법입니다.

독립 실행형 Windows Server의 경우 [X.509 인증서를 사용하여 Windows에서 독립 실행형 클러스터 보안 ](service-fabric-windows-cluster-x509-security.md)

### <a name="node-to-node-windows-security"></a>노드 간 Windows 보안
독립 실행형 Windows Server의 경우 [Windows 보안을 사용하여 Windows에서 독립 실행형 클러스터 보안](service-fabric-windows-cluster-windows-security.md)

## <a name="client-to-node-security"></a>클라이언트-노드 보안
클라이언트를 인증 하 고 클라이언트와 hello 클러스터의 개별 노드 간의 통신을 보호 합니다. 이 유형의 보안 인증 하며 hello 클러스터와 hello 클러스터에 배포 된 hello 응용 프로그램에 권한이 있는 사용자만 액세스할 수 있도록 보장 하는 클라이언트 통신을 보호 합니다. 클라이언트는 Windows 보안 자격 증명이나 인증서 보안 자격 증명을 통해 고유하게 식별됩니다.

![클라이언트-노드 통신의 다이어그램][Client-to-Node]

Azure에서 실행되는 클러스터 또는 Windows에서 실행되는 독립 실행형 클러스터는 [인증서 보안](https://msdn.microsoft.com/library/ff649801.aspx) 또는 [Windows 보안](https://msdn.microsoft.com/library/ff649396.aspx)을 사용할 수 있습니다.

### <a name="client-to-node-certificate-security"></a>클라이언트-노드 인증서 보안
 보안 노드를 클라이언트 인증서는 관리 클라이언트 인증서 및/또는 사용자 클라이언트 인증서를 지정 하 여 hello Azure 포털을 통해, 리소스 관리자 템플릿 또는 독립 실행형 JSON 템플릿 hello 클러스터를 만드는 동안 구성 됩니다.  hello 관리 클라이언트와 사용자 클라이언트 인증서 지정한 계정과 달라 야 hello 기본 및 보조 인증서에 대해 지정한 [노드 보안](#node-to-node-security) 것이 가장 좋습니다. 기본적으로 hello 클러스터 인증서 노드를 보안에 대 한 클라이언트 관리 인증서 목록 허용 toohello를 추가 됩니다.

Hello 관리 인증서를 사용 하 여 toohello 클러스터를 연결 하는 클라이언트에 대 한 모든 권한을 toomanagement 기능이.  Hello 읽기 전용 사용자 클라이언트 인증서를 사용 하 여 toohello 클러스터를 연결 하는 클라이언트 기능이 읽기 권한을 toomanagement. 즉 이러한 인증서는 hello 역할 기반 액세스 제어 (RBAC)이이 문서의 뒷부분에서 설명에 사용 됩니다.

Azure 읽을 [Azure 리소스 관리자 템플릿을 사용 하 여 클러스터를 설정](service-fabric-cluster-creation-via-arm.md) toolearn tooconfigure 클러스터에서 보안 인증서 하는 방법입니다.

독립 실행형 Windows Server의 경우 [X.509 인증서를 사용하여 Windows에서 독립 실행형 클러스터 보안 ](service-fabric-windows-cluster-x509-security.md)

### <a name="client-to-node-azure-active-directory-aad-security-on-azure"></a>Azure에서 클라이언트-노드 AAD(Azure Active Directory) 보안
Azure에서 실행 하는 클러스터 액세스 Azure Active Directory (AAD)를 사용 하 여 toohello 관리 끝점 보안 수도 있습니다. 참조 [Azure 리소스 관리자 템플릿을 사용 하 여 클러스터를 설정](service-fabric-cluster-creation-via-arm.md) toocreate 필요한 AAD 아티팩트 hello 하는 방법에 대 한 내용은 어떻게 toopopulate 시 이러한 클러스터 만들기 및 tooconnect toothose 나중에 클러스터입니다.

## <a name="security-recommendations"></a>보안 권장 사항
Azure의 클러스터에 대 한 노드를 보안에 대 한 AAD tooauthenticate 클라이언트 보안 및 인증서를 사용 것이 좋습니다.

독립 실행형 Windows Server 클러스터의 경우 Windows Server 2012 R2 및 Active Directory가 있는 경우 GMA(그룹 관리 계정)로 Windows 보안을 사용하는 것이 좋습니다. 그렇지 않은 경우 여전히 Windows 계정으로 Windows 보안을 사용합니다.

## <a name="role-based-access-control-rbac"></a>RBAC(역할 기반 액세스 제어)
액세스 제어 작업을 허용 hello 클러스터 관리자 toolimit 액세스 toocertain 클러스터 hello 클러스터를 보안 하는 사용자의 다른 그룹에 대 한 합니다. Tooa 클러스터를 연결 하는 클라이언트에는 두 개의 서로 다른 액세스 제어 형식을 사용할: 관리자 역할 및 사용자 역할입니다.

관리자에 대 한 모든 권한을 toomanagement 기능 (읽기/쓰기 기능만 포함)가 있습니다. 사용자가 기본적으로 읽기 액세스 toomanagement 기능 (예: 쿼리 기능) 및 hello 기능 tooresolve 응용 프로그램 및 서비스입니다.

Hello 관리자 및 사용자 클라이언트 역할 타임 시 지정한 hello 클러스터 생성의 별도 id (인증서, AAD 등)를 제공 하 여 각각에 대 한 합니다. Hello 기본 액세스 제어 설정 및 toochange 기본 설정을 hello 하는 방법에 대 한 자세한 내용은 참조 하십시오. [서비스 패브릭 클라이언트에 대 한 역할 기반 액세스 제어](service-fabric-cluster-security-roles.md)합니다.

## <a name="x509-certificates-and-service-fabric"></a>X.509 인증서 및 서비스 패브릭
X.509 디지털 인증서는 자주 사용 되는 tooauthenticate 클라이언트 및 서버와 tooencrypt와 메시지에 디지털 서명 합니다. 이러한 인증서에 대 한 자세한 내용은 이동 너무[인증서 작업](http://msdn.microsoft.com/library/ms731899.aspx)합니다.

몇 가지 중요 한 사항이 tooconsider:

* 프로덕션 워크로드를 실행하는 클러스터에 사용되는 인증서는 올바르게 구성된 Windows Server 인증서 서비스를 사용하여 만들어지거나 승인된 [CA(인증 기관)](https://en.wikipedia.org/wiki/Certificate_authority)에서 획득해야 합니다.
* 프로덕션 환경에서 MakeCert.exe와 같은 도구를 사용하여 만든 임시 또는 테스트 인증서를 사용하지 마세요.
* 자체 서명된 인증서를 사용할 수 있지만 프로덕션이 아닌 테스트 클러스터에 대해서만 이러한 인증서를 사용해야 합니다.

### <a name="server-x509-certificates"></a>서버 X.509 인증서
서버 인증서가 서버 (노드) tooclients 인증 또는 서버 (노드) tooa 서버 (노드)를 인증의 hello 주요 작업. Hello 초기 검사 노드를 인증 하는 클라이언트 또는 노드 중 하나는 toocheck hello 값 hello hello 제목 필드에 일반 이름입니다. 이 일반 이름 또는 hello 인증서의 주체 대체 이름 중 하나가 hello 허용 된 일반 이름 목록에 있어야 합니다.

hello 다음 문서에서는 설명 toogenerate 주체 대체 이름 (SAN)와 인증서를 어떻게: [tooadd 주체 대체 이름 tooa LDAP 인증서를 보호 하는 방법을](http://support.microsoft.com/kb/931351)합니다.

hello 제목 필드에 여러 값이 포함 될 수 있습니다, 그리고 각 접두사로 추가 하는 초기화 tooindicate hello 값 형식입니다. 가장 일반적으로 hello 초기화는 "CN" 일반 이름;에 대 한 예를 들어 "CN = www.contoso.com"입니다. Hello 제목 필드 toobe 빈 수 이기도합니다. Hello 선택적 주체 대체 이름 필드를 채우면 hello hello 인증서의 일반 이름 및 주체 대체 이름 변수당 하나의 항목이 모두 포함 해야 합니다. 이러한 작업은 DNS 이름 값으로 입력됩니다.

hello 인증서의 hello 용도 필드의 hello 값 "서버 인증" 또는 "클라이언트 인증" 등의 적절 한 값을 포함 해야 합니다.

### <a name="client-x509-certificates"></a>클라이언트 X.509 인증서
클라이언트 인증서는 일반적으로 타사 인증 기관에서 발급되지 않습니다. 대신 hello hello 현재 사용자 위치의 개인 저장소 일반적으로 포함 용도가 "클라이언트 인증"의 루트 인증 기관에서 넣은 클라이언트 인증서입니다. hello 클라이언트 상호 인증이 필요한 경우 이러한 인증서를 사용할 수 있습니다.

> [!NOTE]
> 서비스 패브릭 클러스터의 모든 관리 작업은 서버 인증서가 필요합니다. 관리에 클라이언트 인증서를 사용할 수 없습니다.
> 
> 

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->


## <a name="next-steps"></a>다음 단계
이 문서에서는 클러스터 보안에 대한 개념 정보를 제공합니다. 다음으로,


1.  [Resource Manager 템플릿을 사용하여 Azure에 클러스터 만들기](service-fabric-cluster-creation-via-arm.md) 
2.  [Azure Portal](service-fabric-cluster-creation-via-portal.md).

<!--Image references-->
[Node-to-Node]: ./media/service-fabric-cluster-security/node-to-node.png
[Client-to-Node]: ./media/service-fabric-cluster-security/client-to-node.png
