---
title: "서비스 패브릭 독립 실행형 클러스터 배포 준비 aaaAzure | Microsoft Docs"
description: "설명서 관련 toopreparing hello 환경 고 hello 클러스터 구성을 만들 toobe 간주 이전 toodeploying 프로덕션 작업을 처리 하기 위한 클러스터."
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
ms.openlocfilehash: e503c61a64b408af3f22bd75ab02f1c34ac9f380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
<a id="preparemachines"></a>

## <a name="plan-and-prepare-your-service-fabric-standalone-cluster-deployment"></a>Service Fabric 독립 실행형 클러스터 배포 계획 및 준비
Hello 클러스터를 만들기 전에 다음 단계를 수행 합니다.

### <a name="step-1-plan-your-cluster-infrastructure"></a>1단계: 클러스터 인프라 계획
모르는 toocreate에 대 한 서비스 패브릭 클러스터를 소유 하는 컴퓨터에서 어떤 종류의 오류가 원하는 hello 클러스터 toosurvive 결정할 수도 있습니다. 예를 들어 별도 전원 줄 해야 또는 인터넷 연결 제공 toothese 컴퓨터? 또한 이러한 컴퓨터의 물리적 보안을 hello 것이 좋습니다. Hello 컴퓨터 위치 및 액세스 toothem 인원? 이러한 결정을 내린 후 컴퓨터 toohello hello를 (4 단계 참조)는 다양 한 오류 도메인 논리적으로 매핑할 수 있습니다. hello 인프라 프로덕션 클러스터에 대 한 계획은 테스트 클러스터에 대 한 보다 훨씬 복잡 합니다.

### <a name="step-2-prepare-hello-machines-toomeet-hello-prerequisites"></a>2 단계: 준비 hello 컴퓨터 toomeet hello 필수 구성 요소
사전 요구 사항 각 컴퓨터에 대해 원하는 tooadd toohello 클러스터:

* 최소 16GB의 RAM을 사용하는 것이 좋습니다.
* 최소 40GB의 사용 가능한 디스크 공간이 있는 것이 좋습니다.
* 4코어 이상의 CPU가 권장됩니다.
* 또는 모든 컴퓨터에 대 한 네트워크에 tooa 보안 네트워크를 연결 합니다.
* Windows Server 2012 R2 또는 Windows Server 2016. 
* [.NET Framework 4.5.1 이상](https://www.microsoft.com/download/details.aspx?id=40773), 전체 설치.
* [Windows PowerShell 3.0](https://msdn.microsoft.com/powershell/scripting/setup/installing-windows-powershell).
* hello [RemoteRegistry 서비스](https://technet.microsoft.com/library/cc754820) 모든 hello 컴퓨터에서 실행 되어야 합니다.

hello 클러스터 관리자를 배포 하 고 hello 클러스터 구성 되어 있어야 [관리자 권한이](https://social.technet.microsoft.com/wiki/contents/articles/13436.windows-server-2012-how-to-add-an-account-to-a-local-administrator-group.aspx) 각각의 hello 컴퓨터에서 합니다. 도메인 컨트롤러에 Service Fabric을 설치할 수 없습니다.

### <a name="step-3-determine-hello-initial-cluster-size"></a>3 단계: hello 초기 클러스터 크기를 결정 합니다.
독립 실행형 서비스 패브릭 클러스터의 각 노드는 hello 서비스 패브릭 런타임을 배포 하 고 hello 클러스터의 구성원에 있습니다. 일반적인 프로덕션 배포에서는 OS 인스턴스당(실제 또는 가상) 하나의 노드가 있습니다. hello 클러스터 크기는 비즈니스 요구에 따라 결정 됩니다. 그러나 적어도 세 개 노드의 클러스터 크기가 필요합니다(컴퓨터 또는 가상 컴퓨터).
개발 용도로 지정된 컴퓨터에 하나 이상의 노드를 보유할 수 있습니다. 프로덕션 환경에서 서비스 패브릭은 실제 또는 가상 컴퓨터당 하나의 노드만을 지원합니다.

### <a name="step-4-determine-hello-number-of-fault-domains-and-upgrade-domains"></a>4 단계: hello 장애 도메인 수를 확인 및 업그레이드 도메인
A *장애 도메인* (FD) 물리적 장애 단위 이며 hello 데이터 센터에서 직접 관련된 toohello 물리적 인프라입니다. 장애 도메인은 실패한 단일 지점이 공유하는 하드웨어 구성 요소(컴퓨터, 스위치, 네트워크 등)로 구성됩니다. 쉽게 말해 장애 도메인과 랙 간에 1:1 매핑이 없지만 각 랙은 장애 도메인으로 간주될 수 있습니다. 클러스터의 노드 hello을 고려할 때는 hello 노드 3 개 이상의 오류 도메인 간에 분산 될 것이 좋습니다.

Fd ClusterConfig.json에서를 지정 하면 각 FD에 대 한 hello 이름을 선택할 수 있습니다. 서비스 패브릭은 내부에서 인프라 토폴로지를 반영할 수 있도록 계층적 FD를 지원합니다.  예를 들어 hello Fd 다음 유효한은 같습니다.

* "faultDomain": "fd:/Room1/Rack1/Machine1"
* "faultDomain": "fd:/FD1"
* "faultDomain": "fd:/Room1/Rack1/PDU1/M1"

*UD(업그레이드 도메인)*는 노드의 논리적 단위입니다. 서비스 패브릭 오케스트레이션 업그레이드 (응용 프로그램 업그레이드 또는 클러스터 업그레이드) 하는 동안 한 UD의 모든 노드에서 tooperform hello 업그레이드 노드 다른 Ud에 계속 사용할 수 있는 tooserve 요청 동안 적용 됩니다. hello 컴퓨터에서 수행 하는 펌웨어 업그레이드 인식 하지 않습니다, Ud 하나 해야 하므로 한 번에 컴퓨터입니다.

이러한 개념에 대 한 가장 간단한 방법은 toothink hello hello 단위로 서의 계획 된 유지 관리의 계획 되지 않은 오류 및 Ud hello 단위로 tooconsider Fd 됩니다.

Ud ClusterConfig.json에서를 지정 하면 각 UD hello 이름을 선택할 수 있습니다. 예를 들어 hello 이름 다음 유효한은 같습니다.

* "upgradeDomain": "UD0"
* "upgradeDomain": "UD1A"
* "upgradeDomain": "DomainRed"
* "upgradeDomain": "Blue"

업그레이드 도메인 및 장애 도메인에 대한 자세한 내용은 [Service Fabric 클러스터 설명](service-fabric-cluster-resource-manager-cluster-description.md)을 참조하세요.

### <a name="step-5-download-hello-service-fabric-standalone-package-for-windows-server"></a>5 단계: Windows Server 용 hello 서비스 패브릭 독립 실행형 패키지 다운로드
[다운로드 링크-서비스 패브릭 독립 실행형 패키지-Windows 서버](http://go.microsoft.com/fwlink/?LinkId=730690) 및 hello 패키지의 압축을 푸는 중 하나가 tooa 배포 컴퓨터 즉 hello 클러스터의 일부가 아닌 또는 클러스터의 일부가 될 hello 컴퓨터 tooone을 합니다.

### <a name="step-6-modify-cluster-configuration"></a>6단계: 클러스터 구성 수정
독립 실행형 클러스터 toocreate 해야 toocreate hello 클러스터의 hello 사양을 설명 하는 독립 실행형 클러스터 구성 ClusterConfig.json 파일. Hello 아래 링크에서 찾을 hello 템플릿에 hello 구성 파일을 만들 수 있습니다. <br>
[독립 실행형 클러스터 구성](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)

Hello 섹션이이 파일에 대 한 자세한 내용은 참조 하십시오. [독립 실행형 Windows 클러스터에 대 한 구성 설정을](service-fabric-cluster-manifest.md)합니다.

Hello ClusterConfig.json 파일 중 하나에서 다운로드 한 hello 패키지 열고 hello 다음 설정을 수정 합니다.
| **구성 설정** | **설명** |
| --- | --- |
| **NodeTypes** |노드 형식을 사용 하면 tooseparate 다양 한 그룹으로 클러스터 노드. 클러스터에는 하나 이상이 NodeType이 있어야 합니다. 그룹의 모든 노드는 공통적인 특성은 다음 hello: <br> **이름** -hello 노드 형식 이름입니다. <br>**끝점 포트** - 이 노드 유형과 연결된 다양한 이름의 끝점(포트)입니다. 이 매니페스트의 다른 요소와 충돌 하지 않는 상태로 원하는 지 이미 VM/hello 컴퓨터에서 실행 중인 다른 응용 프로그램에서 사용 하는 임의의 포트 번호를 사용할 수 있습니다. <br> **배치 속성** -이러한 hello 시스템 서비스 또는 서비스에 대 한 배치 제약 조건으로 사용 하는이 노드 형식에 대 한 속성에 설명 합니다. 이런 속성은 주어진 노드에 대한 여분의 메타데이터를 제공하는 사용자 정의 키/값 쌍입니다. 노드 속성의 예로 hello 노드의 하드 드라이브 또는 그래픽 카드, 스핀 들의 하드 디스크, 코어, 그리고 다른 물리적 속성 수가 hello에 있는지 여부는 것입니다. <br> **용량** -hello 이름 및 특정 리소스의 양에 노드 용량 정의 특정 노드에 소비에 사용할 수 있는 합니다. 예를 들어 노드에는 "MemoryInMb"라는 메트릭에 대한 용량 및 기본적으로 사용할 수 있는 2048MB가 있음을 정의할 수 있습니다. 이러한 용량 런타임 tooensure 특정 양의 리소스를 필요로 하는 서비스는 저장 하는 hello 노드에서 hello에서 사용할 수 있는 이러한 리소스 필요한 금액에 사용 됩니다.<br>**IsPrimary** -하나 이상 정의 된 노드 유형의 하나만 tooprimary hello 값으로 설정 되어 있는지 확인 해야 하는 경우 *true*, hello 시스템 서비스가 실행 되는 합니다. 다른 모든 노드 형식은 toohello 값 설정 해야 *false* |
| **노드** |이들은 hello 노드 (노드 유형, 노드 이름, IP 주소, 장애 도메인 및 업그레이드 도메인 hello 노드의) hello 클러스터의 일부인 각 hello 세부 정보입니다. hello 컴퓨터 원하는 hello 클러스터 toobe 필요 toobe 해당 IP 주소와 함께 나열에 생성 합니다. <br> Hello를 사용 하는 경우 동일한 IP 주소 모든 hello 노드에 대 한 테스트 목적으로 사용할 수 있는 한 기본 클러스터를 만들 합니다. one-box 클러스터는 프로덕션 워크로드를 배포하는 데 사용하지 마세요. |

Hello 클러스터 구성에는 모든 구성 된 설정을 toohello 환경 가진, hello 클러스터 환경 (단계 7)에 대해 테스트할 수 있습니다.

<a id="environmentsetup"></a>

### <a name="step-7-environment-setup"></a>7단계. 환경 설정

클러스터 관리자는 독립 실행형 서비스 패브릭 클러스터를 구성할 때 hello 환경은 필요 toobe 조건 다음 hello를 사용 하 여 설정: <br>
1. hello 클러스터를 만드는 hello 사용자 hello 클러스터 구성 파일에 있는 노드로 나열 되는 관리자 수준의 보안 권한 tooall 컴퓨터 있어야 합니다.
2. 각 클러스터 노드 컴퓨터 뿐만 아니라 어떤 hello에서 클러스터를 만든 컴퓨터 수행 해야 합니다.
* Service Fabric SDK 제거
* Service Fabric 런타임 제거 
* Hello Windows 방화벽 서비스 (mpssvc) 사용 하도록 설정한
* 원격 레지스트리 서비스 (remoteregistry) hello 설정한
* 파일 공유(SMB) 활성화
* 클러스터 구성 포트에 따라 필요한 포트 열기
* Windows SMB 및 원격 레지스트리 서비스: 135, 137, 138, 139 및 445에 대한 필요한 포트 열기
* 네트워크 연결 tooone가 다른
3. None hello 클러스터 노드 컴퓨터의 도메인 컨트롤러 여야 합니다.
4. 배포 된 hello 클러스터 toobe 보안 클러스터 일 경우 hello 필요한 보안의 필수 구성 요소가 놓고 hello 구성에 대해 올바르게 구성 되었는지 확인 합니다.
5. Hello 클러스터 컴퓨터의 인터넷 액세스가 불가능 하면 hello에서 집합 hello 다음 클러스터 구성:
* 원격 분석 사용 안 함: *속성*에서 *“enableTelemetry”: false* 설정
* 자동 패브릭 버전을 다운로드 및 해당 hello 현재 클러스터 버전 지원 종료에 거의 도달 알림 사용 안 함: 아래 *속성* 설정 *"fabricClusterAutoupgradeEnabled": false*
* 또는 네트워크 인터넷 액세스가 제한 된 toowhite 나열 된 도메인, hello 도메인 아래에 필요한 지 여부 자동 업그레이드: go.microsoft.com download.microsoft.com

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
hello TestConfiguration.ps1 스크립트 hello 독립 실행형 패키지에서 찾을 수 있습니다. hello 기준 위의 몇 가지 모범 사례 분석기 toovalidate로 사용 되며 지정된 된 환경에는 클러스터를 배포할 수 있는지 여부를 온전성 검사 toovalidate로 사용 하시기 바랍니다. 모든 오류가 있으면 참조 아래의 toohello 목록 [환경 설치](service-fabric-cluster-standalone-deployment-preparation.md) 문제 해결에 대 한 합니다. 

이 스크립트는 관리자 액세스 tooall hello 컴퓨터 노드로 hello 클러스터 구성 파일에 나열 된 모든 컴퓨터에서 실행할 수 있습니다. 이 스크립트에서 실행 되는 hello 컴퓨터에는 hello 클러스터의 일부가 toobe 없습니다.

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
Trace folder already exists. Traces will be written tooexisting trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
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

현재이 구성을 테스트 모듈 toobe 독립적으로 수행 되므로이 hello 보안 구성을 확인 하지 않습니다.  

> [!NOTE]
> 계속 해 서 진행 중인 개선 toomake이이 모듈 보다 강력한, 따라서는 결함이 있거나 경우 TestConfiguration 하 여 현재 동기화 되지 않는다고 판단 되는 항목이 없습니다, 알려 주시면 통해 우리의 [채널을 지원](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support)합니다.   
> 
> 

## <a name="next-steps"></a>다음 단계
* [Windows Server에서 실행되는 독립 실행형 클러스터 만들기](service-fabric-cluster-creation-for-windows-server.md)
