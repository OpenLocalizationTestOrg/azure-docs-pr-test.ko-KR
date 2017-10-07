---
title: "Windows 보안을 사용 하 여 Windows에서 실행 중인 클러스터 a는 aaaSecure | Microsoft Docs"
description: "독립 실행형 tooconfigure 노드와 노드 및 노드 클라이언트 보안 클러스터 Windows 보안을 사용 하 여 Windows에서 실행 하는 방법을 알아봅니다."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: ce3bf686-ffc4-452f-b15a-3c812aa9e672
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: dekapur
ms.openlocfilehash: 44f3011eb630357f342052a48d6c852b17dccec4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-standalone-cluster-on-windows-by-using-windows-security"></a>Windows 보안을 사용하여 독립 실행형 클러스터 보호
tooprevent 무단 액세스 tooa 서비스 패브릭 클러스터, hello 클러스터를 보호 해야 합니다. 보안은 hello 클러스터 프로덕션 워크 로드를 실행 하는 경우에 특히 중요 합니다. 이 문서에서는 설명 방법을 hello의 Windows 보안을 사용 하 여 tooconfigure 노드와 노드 및 노드 클라이언트 보안 *ClusterConfig.JSON* 파일입니다.  hello 프로세스 toohello 해당 구성의 보안 단계 [Windows에서 실행 되는 독립 실행형 클러스터 만들기](service-fabric-cluster-creation-for-windows-server.md)합니다. Service Fabric에서 Windows 보안을 사용하는 방법에 대한 자세한 내용은 [클러스터 보안 시나리오](service-fabric-cluster-security.md)를 참조하세요.

> [!NOTE]
> 하나의 보안 선택 tooanother에서 클러스터 업그레이드가 지원 되지 않으므로 hello 선택의 노드 보안을 신중 하 게 고려해 야 합니다. toochange hello 보안 선택 toorebuild hello 전체 클러스터를 해야합니다.
>
>

## <a name="configure-windows-security-using-gmsa"></a>gMSA를 사용하여 Windows 보안 구성  
hello 샘플 *ClusterConfig.gMSA.Windows.MultiMachine.JSON* hello로 구성 파일을 다운로드할 [Microsoft.Azure.ServiceFabric.WindowsServer.<version>합니다. zip](http://go.microsoft.com/fwlink/?LinkId=730690) 사용 하 여 Windows 보안을 구성 하기 위한 서식 파일을 포함 하는 독립 실행형 클러스터 패키지 [그룹 관리 서비스 계정 (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):  

```  
"security": {  
            "WindowsIdentities": {  
                "ClustergMSAIdentity": "accountname@fqdn"  
                "ClusterSPN": "fqdn"  
                "ClientIdentities": [  
                    {  
                        "Identity": "domain\\username",  
                        "IsAdmin": true  
                    }  
                ]  
            }  
        }  
```  
  
| **구성 설정** | **설명** |  
| --- | --- |  
| WindowsIdentities |Hello 클러스터 및 클라이언트 id를 포함합니다. |  
| ClustergMSAIdentity |노드 간 보안을 구성합니다. 그룹 관리 서비스 계정입니다. |  
| ClusterSPN |gMSA 계정에 대한 정규화된 도메인 SPN|  
| ClientIdentities |클라이언트-노드 보안을 구성합니다. 클라이언트 사용자 계정의 배열입니다. |  
| ID |도메인 사용자 hello 클라이언트 id입니다. |  
| IsAdmin |True 해당 hello 도메인 사용자가 관리자가 클라이언트 액세스, 사용자 클라이언트 액세스에 대해 false를 지정 합니다. |  
  
[노드 toonode 보안](service-fabric-cluster-security.md#node-to-node-security) 설정 하 여 구성 된 **ClustergMSAIdentity** 서비스 패브릭 toorun gMSA에서 필요로 하는 경우. 노드 간 순서 toobuild 트러스트 관계에 있도록 해야 서로 인식 합니다. 이 두 가지 방법으로 수행할 수 있습니다: 그룹 관리 서비스 계정을 hello 클러스터의 모든 노드를 포함 하는 hello를 지정 하거나 hello 클러스터의 모든 노드를 포함 하는 hello 도메인 컴퓨터 그룹을 지정 합니다. Hello를 사용 하는 것이 좋습니다 [그룹 관리 서비스 계정 (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) 가능성이 toogrow 되거나 축소 된 클러스터 또는 더 큰 클러스터 (10 개 이상의 노드)에 대 한 특히 방법을 사용 합니다.  
이 방법은 hello 만들 도메인 그룹을 클러스터 관리자 액세스 권한 tooadd 부여 되 고 구성원을 제거 하지 않아도 됩니다. 이러한 계정은 자동 암호 관리에도 유용합니다. 자세한 내용은 [그룹 관리 서비스 계정 시작](http://technet.microsoft.com/library/jj128431.aspx)을 참조하세요.  
 
[클라이언트 toonode 보안](service-fabric-cluster-security.md#client-to-node-security) 를 사용 하 여 구성 된 **ClientIdentities**합니다. 클라이언트와 hello 클러스터 간의 순서 tooestablish 신뢰 hello 클러스터 tooknow 신뢰할 수 있는 클라이언트 id를 구성 해야 합니다. 두 가지 방법으로이 작업을 수행할 수 있습니다: hello 도메인 그룹 사용자 지정 하거나 연결할 수 있는 hello 도메인 노드 사용자 연결 수를 지정 합니다. 서비스 패브릭 연결된 tooa 서비스 패브릭 클러스터에 있는 클라이언트에 대 한 두 개의 서로 다른 액세스 제어 유형을 지원: 관리자와 사용자입니다. 액세스 제어는 클러스터 관리자 toolimit 액세스 toocertain 유형의 클러스터 작업이 서로 다른 hello 클러스터를 보안 하는 사용자, 그룹에 대 한 hello에 대 한 hello 기능을 제공 합니다.  관리자에 대 한 모든 권한을 toomanagement 기능 (읽기/쓰기 기능만 포함)가 있습니다. 사용자가 기본적으로 읽기 액세스 toomanagement 기능 (예: 쿼리 기능) 및 hello 기능 tooresolve 응용 프로그램 및 서비스입니다. 액세스 제어에 대한 자세한 내용은 [Service Fabric 클라이언트의 역할 기반 액세스 제어](service-fabric-cluster-security-roles.md)를 참조하세요.  
 
다음 예에서는 hello **보안** gMSA를 사용 하 여 Windows 보안을 구성 하 고 해당 hello에 컴퓨터를 지정 하는 섹션 *ServiceFabric.clusterA.contoso.com* gMSA hello 클러스터의 일부인 *CONTOSO\usera* 관리자 클라이언트 권한이 있습니다.  
  
```  
"security": {  
    "WindowsIdentities": {  
        "ClustergMSAIdentity" : "ServiceFabric.clusterA.contoso.com",  
        "ClusterSPN" : "clusterA.contoso.com",  
        "ClientIdentities": [{  
            "Identity": "CONTOSO\\usera",  
            "IsAdmin": true  
        }]  
    }  
}  
```  
  
## <a name="configure-windows-security-using-a-machine-group"></a>컴퓨터 그룹을 사용하여 Windows 보안 구성  
hello 샘플 *ClusterConfig.Windows.MultiMachine.JSON* hello로 구성 파일을 다운로드할 [Microsoft.Azure.ServiceFabric.WindowsServer.<version>합니다. zip](http://go.microsoft.com/fwlink/?LinkId=730690) 독립 실행형 클러스터 패키지의 Windows 보안 구성에 대 한 템플릿을 포함 합니다.  Windows 보안 hello에 구성 되어 **속성** 섹션: 

```
"security": {
            "ClusterCredentialType": "Windows",
            "ServerCredentialType": "Windows",
            "WindowsIdentities": {
                "ClusterIdentity" : "[domain\machinegroup]",
                "ClientIdentities": [{
                    "Identity": "[domain\username]",
                    "IsAdmin": true
                }]
            }
        }
```

| **구성 설정** | **설명** |
| --- | --- |
| ClusterCredentialType |**ClusterCredentialType** 너무 설정*Windows* ClusterIdentity은 Active Directory 시스템 그룹 이름을 지정 하는 경우. |  
| ServerCredentialType |도*Windows* tooenable 클라이언트에 대 한 Windows 보안 합니다.<br /><br />이 hello 클라이언트 hello 클러스터와 hello 클러스터 자체의 Active Directory 도메인 내에서 실행 되 고 있는지 나타냅니다. |  
| WindowsIdentities |Hello 클러스터 및 클라이언트 id를 포함합니다. |  
| ClusterIdentity |컴퓨터 그룹 이름, domain\machinegroup, tooconfigure 노드 보안을 사용 합니다. |  
| ClientIdentities |클라이언트-노드 보안을 구성합니다. 클라이언트 사용자 계정의 배열입니다. |  
| ID |도메인 \ 사용자 이름 hello 클라이언트 id에 대 한 hello 도메인 사용자를 추가 합니다. |  
| IsAdmin |도메인 사용자 hello 집합 tootrue toospecify에 관리자가 클라이언트 액세스 또는 사용자 클라이언트 액세스에 대해서는 false입니다. |  

[노드 toonode 보안](service-fabric-cluster-security.md#node-to-node-security) 설정을 사용 하 여 구성 된 **ClusterIdentity** toouse Active Directory 도메인 내에서 컴퓨터 그룹을 선택 합니다. 자세한 내용은 [Active Directory에 컴퓨터 그룹 만들기](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx)를 참조하세요.

[클라이언트-노드 간 보안](service-fabric-cluster-security.md#client-to-node-security)은 **ClientIdentities**를 사용하여 구성됩니다. 클라이언트와 hello 클러스터 간 트러스트 tooestablish는 hello 클러스터 tooknow hello 클라이언트를 신뢰할 수 있는 클러스터 hello 하는 id를 구성 해야 합니다. 다음 두 가지 방법으로 트러스트를 설정할 수 있습니다.

- 연결할 수 있는 hello 도메인 그룹 사용자가 지정 합니다.
- 연결할 수 있는 hello 도메인 노드 사용자 지정 합니다.

서비스 패브릭 연결된 tooa 서비스 패브릭 클러스터에 있는 클라이언트에 대 한 두 개의 서로 다른 액세스 제어 유형을 지원: 관리자와 사용자입니다. 액세스 제어 하면 hello 클러스터 관리자 toolimit 액세스 toocertain 형식을 서로 다른 사용자를 그룹에 대 한 클러스터 작업의 수 있게 해줍니다 hello 클러스터 더 안전 합니다.  관리자에 대 한 모든 권한을 toomanagement 기능 (읽기/쓰기 기능만 포함)가 있습니다. 사용자가 기본적으로 읽기 액세스 toomanagement 기능 (예: 쿼리 기능) 및 hello 기능 tooresolve 응용 프로그램 및 서비스입니다.  

다음 예에서는 hello **보안** 섹션 Windows 보안을 구성 하며, 해당 hello 컴퓨터에서 지정 *ServiceFabric/clusterA.contoso.com* hello 클러스터의 일부 이며 해당 지정 *CONTOSO\usera* 관리자 클라이언트 권한이 있습니다.

```
"security": {
    "ClusterCredentialType": "Windows",
    "ServerCredentialType": "Windows",
    "WindowsIdentities": {
        "ClusterIdentity" : "ServiceFabric/clusterA.contoso.com",
        "ClientIdentities": [{
            "Identity": "CONTOSO\\usera",
            "IsAdmin": true
        }]
    }
},
```

> [!NOTE]
> 도메인 컨트롤러에 Service Fabric을 배포해서는 안 됩니다. ClusterConfig.json 컴퓨터 그룹을 사용 하는 경우 hello 도메인 컨트롤러의 hello IP 주소를 포함 하거나 그룹 관리 서비스 계정 (gMSA) 하지 않는 있는지 확인 합니다.
>
>

## <a name="next-steps"></a>다음 단계
Hello에서 Windows 보안을 구성한 후 *ClusterConfig.JSON* 파일, hello 클러스터를 만드는 프로세스를 다시 시작 [Windows에서 실행 되는 독립 실행형 클러스터 만들기](service-fabric-cluster-creation-for-windows-server.md)합니다.

노드 간 보안, 클라이언트 및 노드 간 보안 및 역할 기반 액세스 제어 방법에 대한 자세한 내용은 [클러스터 보안 시나리오](service-fabric-cluster-security.md)를 참조하세요.

참조 [연결 tooa 보안 클러스터](service-fabric-connect-to-secure-cluster.md) FabricClient 또는 PowerShell을 사용 하 여 연결에 대 한 예제입니다.
