---
title: "Azure Service Fabric 독립 실행형 클러스터 배포 준비 | Microsoft Docs"
description: "프로덕션 워크로드를 처리하기 위한 클러스터를 배포하기 전에 고려해야 하는 환경 준비 및 클러스터 구성 만들기와 관련된 설명서입니다."
services: service-fabric
documentationcenter: .net
author: maburlik
manager: timlt
editor: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 1/17/2017
ms.author: maburlik;chackdan
ms.openlocfilehash: f332193f9a53260173a1010b8bf9f08726bea427
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
<a id="preparemachines"></a>

## <a name="plan-and-prepare-your-service-fabric-standalone-cluster-deployment"></a>Service Fabric 독립 실행형 클러스터 배포 계획 및 준비
클러스터를 만들기 전에 다음 단계를 수행합니다.

### <a name="step-1-plan-your-cluster-infrastructure"></a>1단계: 클러스터 인프라 계획
클러스터가 견뎌낼 수 있는 실패의 종류를 결정할 수 있도록 소유한 컴퓨터에서 서비스 패브릭 클러스터를 만들려고 합니다. 예를 들어 이러한 컴퓨터를 제공하는 전원 줄 또는 인터넷 연결을 구분해야 하나요? 또한 이러한 컴퓨터의 물리적 보안을 고려합니다. 컴퓨터는 어디에 있으며 누가 액세스해야 하나요? 이러한 결정을 내리면 다양한 오류 도메인에 컴퓨터를 논리적으로 매핑할 수 있습니다(4단계 참조). 프로덕션 클러스터에 대한 인프라 계획은 테스트 클러스터보다 더 복잡합니다.

### <a name="step-2-prepare-the-machines-to-meet-the-prerequisites"></a>2단계: 컴퓨터를 준비하여 필수 구성 요소 충족
클러스터에 추가하려는 각 컴퓨터에 대한 필수 구성 요소:

* 최소 16GB의 RAM을 사용하는 것이 좋습니다.
* 최소 40GB의 사용 가능한 디스크 공간이 있는 것이 좋습니다.
* 4코어 이상의 CPU가 권장됩니다.
* 모든 컴퓨터가 보안 네트워크에 연결되어 있습니다.
* Windows Server 2012 R2 또는 Windows Server 2016. 
* [.NET Framework 4.5.1 이상](https://www.microsoft.com/download/details.aspx?id=40773), 전체 설치.
* [Windows PowerShell 3.0](https://msdn.microsoft.com/powershell/scripting/setup/installing-windows-powershell).
* [RemoteRegistry 서비스](https://technet.microsoft.com/library/cc754820) 는 모든 컴퓨터에서 실행되어야 합니다.

클러스터를 배포하고 구성하는 클러스터 관리자는 각 컴퓨터에서 [관리자 권한](https://social.technet.microsoft.com/wiki/contents/articles/13436.windows-server-2012-how-to-add-an-account-to-a-local-administrator-group.aspx) 이 있어야 합니다. 도메인 컨트롤러에 Service Fabric을 설치할 수 없습니다.

### <a name="step-3-determine-the-initial-cluster-size"></a>3단계: 초기 클러스터 크기 결정
독립 실행형 Service Fabric 클러스터에 있는 각 노드는 배포된 Service Fabric 런타임을 가지며 클러스터의 구성원입니다. 일반적인 프로덕션 배포에서는 OS 인스턴스당(실제 또는 가상) 하나의 노드가 있습니다. 클러스터 크기는 비즈니스 요구에 따라 결정됩니다. 그러나 적어도 세 개 노드의 클러스터 크기가 필요합니다(컴퓨터 또는 가상 컴퓨터).
개발 용도로 지정된 컴퓨터에 하나 이상의 노드를 보유할 수 있습니다. 프로덕션 환경에서 서비스 패브릭은 실제 또는 가상 컴퓨터당 하나의 노드만을 지원합니다.

### <a name="step-4-determine-the-number-of-fault-domains-and-upgrade-domains"></a>4단계: 장애 도메인 및 업그레이드 도메인 수 확인
*FD(장애 도메인)*는 실패의 물리적 단위이며 데이터 센터의 물리적 인프라에 직접 연관됩니다. 장애 도메인은 실패한 단일 지점이 공유하는 하드웨어 구성 요소(컴퓨터, 스위치, 네트워크 등)로 구성됩니다. 쉽게 말해 장애 도메인과 랙 간에 1:1 매핑이 없지만 각 랙은 장애 도메인으로 간주될 수 있습니다. 클러스터에서 노드를 고려하는 경우 노드가 세 개 이상의 장애 도메인에 배포되는 것이 좋습니다.

FD를 ClusterConfig.json에 지정하는 경우 각 FD의 이름을 선택할 수 있습니다. 서비스 패브릭은 내부에서 인프라 토폴로지를 반영할 수 있도록 계층적 FD를 지원합니다.  예를 들어 다음 FD가 유효합니다.

* "faultDomain": "fd:/Room1/Rack1/Machine1"
* "faultDomain": "fd:/FD1"
* "faultDomain": "fd:/Room1/Rack1/PDU1/M1"

*UD(업그레이드 도메인)*는 노드의 논리적 단위입니다. Service Fabric이 업그레이드(응용 프로그램 업그레이드 또는 클러스터 업그레이드)를 조정하는 동안 다른 UD의 노드를 요청을 처리하는 데 계속 사용할 수 있도록 업그레이드를 수행하기 위해 UD의 모든 노드를 사용합니다. 컴퓨터에 수행하는 펌웨어 업그레이드는 UD를 인식하지 못하므로 한 번에 하나의 컴퓨터를 수행해야 합니다.

이러한 개념에 대해 생각하는 가장 간단한 방법은 FD를 계획되지 않은 오류의 단위로, UD를 계획된 유지 관리의 단위로 인식하는 것입니다.

UD를 ClusterConfig.json에 지정하는 경우 각 UD의 이름을 선택할 수 있습니다. 예를 들어 다음 이름이 유효합니다.

* "upgradeDomain": "UD0"
* "upgradeDomain": "UD1A"
* "upgradeDomain": "DomainRed"
* "upgradeDomain": "Blue"

업그레이드 도메인 및 장애 도메인에 대한 자세한 내용은 [Service Fabric 클러스터 설명](service-fabric-cluster-resource-manager-cluster-description.md)을 참조하세요.

### <a name="step-5-download-the-service-fabric-standalone-package-for-windows-server"></a>5단계: Windows Server용 서비스 패브릭 독립 실행형 패키지 다운로드
[다운로드 링크 - Service Fabric 독립 실행형 패키지 -Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690), 클러스터의 일부가 아닌 배포 컴퓨터 또는 클러스터의 일부인 컴퓨터 중 하나에 패키지의 압축을 풉니다.

### <a name="step-6-modify-cluster-configuration"></a>6단계: 클러스터 구성 수정
독립 실행형 클러스터를 만들려면 클러스터의 사양을 설명하는 독립 실행형 클러스터 구성 ClusterConfig.json 파일을 만들어야 합니다. 아래 링크에서 찾을 수 있는 템플릿의 구성 파일을 기반으로 할 수 있습니다. <br>
[독립 실행형 클러스터 구성](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)

이 파일의 섹션에 대한 자세한 내용은 [독립 실행형 Windows 클러스터에 대한 구성 설정](service-fabric-cluster-manifest.md)을 참조하세요.

다운로드한 패키지에서 ClusterConfig.json 파일 중 하나를 열고 다음 설정을 수정합니다.
| **구성 설정** | **설명** |
| --- | --- |
| **NodeTypes** |노드 유형을 사용하면 클러스터 노드를 다양한 그룹으로 구분할 수 있습니다. 클러스터에는 하나 이상이 NodeType이 있어야 합니다. 그룹의 모든 노드는 다음과 같은 일반적인 특징이 있습니다. <br> **이름** - 노드 유형 이름입니다. <br>**끝점 포트** - 이 노드 유형과 연결된 다양한 이름의 끝점(포트)입니다. 이 매니페스트의 다른 요소와 충돌하지 않으며 컴퓨터/VM에서 실행 중인 다른 응용 프로그램에서 사용하지 않는 한 원하는 모든 포트 번호를 사용할 수 있습니다. <br> **배치 속성** - 이는 시스템 서비스 또는 서비스에 대한 배치 제약 조건으로 사용할 다음 노드 유형에 대한 속성을 설명합니다. 이런 속성은 주어진 노드에 대한 여분의 메타데이터를 제공하는 사용자 정의 키/값 쌍입니다. 노드 속성의 예로는 노드에 하드 드라이브 또는 그래픽 카드가 있는지 여부, 하드 드라이브, 코어에 포함된 스핀들 수, 기타 물리 속성이 있습니다. <br> **용량** - 노드 용량은 특정 노드가 사용할 수 있는 특정 리소스의 이름과 양을 정의합니다. 예를 들어 노드에는 "MemoryInMb"라는 메트릭에 대한 용량 및 기본적으로 사용할 수 있는 2048MB가 있음을 정의할 수 있습니다. 이러한 용량은 특정한 양의 리소스를 필요로 하는 서비스가 해당 리소스가 필요한 양만큼 사용 가능한 노드에 배치되도록 런타임 시 사용됩니다.<br>**IsPrimary** - 둘 이상의 NodeType이 정의되어 있으면 하나만 기본으로 설정되어 있는지 확인합니다(값 *true* 지정). 이러한 기본 유형에서 시스템 서비스가 실행됩니다. 다른 모든 노드 유형은 *false* 값으로 설정되어야 합니다. |
| **노드** |클러스터의 일부인 노드 각각에 대한 세부 정보입니다(노드 유형, 노드 이름, IP 주소, 노드의 장애 도메인 및 업그레이드 도메인). 클러스터를 만들려는 컴퓨터는 여기서 해당 IP 주소로 나열되어야 합니다. <br> 모든 노드에 동일한 IP 주소를 사용하는 경우 다음 one-box 클러스터가 만들어지며 테스트를 목적으로 사용할 수 있습니다. one-box 클러스터는 프로덕션 워크로드를 배포하는 데 사용하지 마세요. |

클러스터 구성에서 모든 설정을 환경에 구성한 후 클러스터 환경에 대해 테스트할 수 있습니다(7단계).

<a id="environmentsetup"></a>

### <a name="step-7-environment-setup"></a>7단계. 환경 설정

클러스터 관리자가 Service Fabric 독립 실행형 클러스터를 구성할 때 환경은 다음 기준으로 설정되어야 합니다. <br>
1. 클러스터를 만드는 사용자에는 클러스터 구성 파일에서 노드로 나열된 모든 컴퓨터에 대한 관리자 수준 보안 권한이 있어야 합니다.
2. 클러스터가 생성되는 컴퓨터 뿐 아니라 각 클러스터 노드 컴퓨터는 다음이 필수입니다.
* Service Fabric SDK 제거
* Service Fabric 런타임 제거 
* Windows 방화벽 서비스(mpssvc) 활성화
* 원격 레지스트리 서비스(remoteregistry) 활성화
* 파일 공유(SMB) 활성화
* 클러스터 구성 포트에 따라 필요한 포트 열기
* Windows SMB 및 원격 레지스트리 서비스: 135, 137, 138, 139 및 445에 대한 필요한 포트 열기
* 네트워크 간 연결
3. 모든 클러스터 노드 컴퓨터는 도메인 컨트롤러여서는 안 됩니다.
4. 배포되는 클러스터가 보안 클러스터인 경우 필수 보안 구성 요소가 배치되고 구성에 대해 올바르게 구성되어 있는지 유효성을 검사합니다.
5. 클러스터 컴퓨터를 인터넷에서 액세스할 수 없는 경우 클러스터 구성에서 다음을 설정합니다.
* 원격 분석 사용 안 함: *속성*에서 *“enableTelemetry”: false* 설정
* 자동 패브릭 버전 다운로드 및 현재 클러스터 버전이 곧 지원 종료된다는 알림 사용 안 함: *속성*에서 *“fabricClusterAutoupgradeEnabled”: false* 설정
* 또는 네트워크 인터넷 액세스가 허용 목록 도메인으로 제한될 경우 자동 업그레이드를 위해 도메인 go.microsoft.com   download.microsoft.com이 필요합니다.

6. 적절한 Service Fabric 바이러스 백신 예외 설정:

| **바이러스 백신 제외된 디렉터리** |
| --- |
| Program Files\Microsoft Service Fabric |
| FabricDataRoot(클러스터 구성에서) |
| FabricLogRoot(클러스터 구성에서) |

| **바이러스 백신 제외된 프로세스** |
| --- |
| Fabric.exe |
| FabricHost.exe |
| FabricInstallerService.exe |
| FabricSetup.exe |
| FabricDeployer.exe |
| ImageBuilder.exe |
| FabricGateway.exe |
| FabricDCA.exe |
| FabricFAS.exe |
| FabricUOS.exe |
| FabricRM.exe |
| FileStoreService.exe |

### <a name="step-8-validate-environment-using-testconfiguration-script"></a>8단계: TestConfiguration 스크립트를 사용하여 환경 유효성 검사
TestConfiguration.ps1 스크립트는 독립 실행형 패키지에서 찾을 수 있습니다. 위의 조건 중 일부의 유효성을 검사하는 모범 사례 분석기로 사용되며 지정된 환경에 클러스터를 배포할 수 있는지 여부를 확인하는 온전성 검사로 사용되어야 합니다. 오류가 있는 경우 문제 해결은 [환경 설치](service-fabric-cluster-standalone-deployment-preparation.md) 아래의 목록을 참조하세요. 

이 스크립트는 클러스터 구성 파일에서 노드로 나열된 모든 컴퓨터에 대한 관리자 액세스 권한이 있는 모든 컴퓨터에서 실행될 수 있습니다. 이 스크립트가 실행되는 컴퓨터가 클러스터의 일부일 필요는 없습니다.

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
Trace folder already exists. Traces will be written to existing trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
Running Best Practices Analyzer...
Best Practices Analyzer completed successfully.


LocalAdminPrivilege        : True
IsJsonValid                : True
IsCabValid                 : True
RequiredPortsOpen          : True
RemoteRegistryAvailable    : True
FirewallAvailable          : True
RpcCheckPassed             : True
NoConflictingInstallations : True
FabricInstallable          : True
Passed                     : True
```

현재 이 구성 테스트 모듈은 보안 구성을 확인하지 않으므로 독립적으로 수행되어야 합니다.  

> [!NOTE]
> 이 모듈을 더욱 강력하게 만들도록 계속해서 개선하고 있으므로 현재 TestConfiguration에서 감지하지 못한다고 생각하는 결함 또는 누락된 사례가 있는 경우 [지원 채널](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support)을 통해 알려 주세요.   
> 
> 

## <a name="next-steps"></a>다음 단계
* [Windows Server에서 실행되는 독립 실행형 클러스터 만들기](service-fabric-cluster-creation-for-windows-server.md)
