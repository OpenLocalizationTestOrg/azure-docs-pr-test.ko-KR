---
title: "Windows를 실행 하는 Azure Vm과 aaaCreate 독립 실행형 클러스터 | Microsoft Docs"
description: "자세한 내용은 방법 toocreate 및 Windows Server를 실행 하는 Azure 가상 컴퓨터에는 Azure 서비스 패브릭 클러스터를 관리 합니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 7eeb40d2-fb22-4a77-80ca-f1b46b22edbc
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: ryanwi;chackdan
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: 8900204fe69887a7a0ca54b06e0d32534421bcfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-three-node-standalone-service-fabric-cluster-with-azure-virtual-machines-running-windows-server"></a>Windows Server를 실행하는 Azure 가상 컴퓨터에서 세 개 노드의 독립 실행형 서비스 패브릭 클러스터 만들기
이 문서에서는 Windows 기반 Azure 가상 컴퓨터 (Vm)에서 클러스터 a toocreate에 대 한 독립 실행형 서비스 패브릭 설치 관리자를 사용 하 여 hello 하는 방법을 설명 합니다. Windows Server. hello 시나리오는 특수 한 경우 [만들기 및 Windows Server에서 실행 하는 클러스터 관리](service-fabric-cluster-creation-for-windows-server.md) hello Vm이 있는 [Windows Server를 실행 하는 Azure Vm](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)만들지 않는 있지만, [Azure 클라우드 기반 서비스 패브릭 클러스터](service-fabric-cluster-creation-via-portal.md)합니다. 이 패턴을 따르면에 hello 차이 hello Azure 클라우드 기반 서비스 패브릭 클러스터를 관리 하 고 hello 서비스 패브릭에서 업그레이드 하는 반면 사용자가 해당 hello 독립 실행형 서비스 패브릭 클러스터 hello 단계에서 만든 완전히 관리 되는 리소스 공급자입니다.

## <a name="steps-toocreate-hello-standalone-cluster"></a>단계 toocreate hello 독립 실행형 클러스터
1. Azure 포털 toohello 하 고 리소스 그룹에 새 Windows Server 2012 R2 Datacenter 또는 Windows Server 2016 데이터 센터 VM을 만들 합니다. Hello 문서 읽기 [hello Azure 포털에서에서 Windows VM을 만듭니다](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 내용을 확인 합니다.
2. 몇 가지 더 많은 Vm toohello 추가 동일한 리소스 그룹입니다. 관리자 사용자 이름 및 암호를 만들 때 동일한 hello에 각각 hello Vm 확인 합니다. 일단 만들어지고 hello에서 모든 세 개의 Vm이 표시 되어야 동일한 가상 네트워크입니다.
3. Hello Vm의 tooeach 연결 하 고 hello hello를 사용 하 여 Windows 방화벽 해제 [서버 관리자에서 로컬 서버 대시보드](https://technet.microsoft.com/library/jj134147.aspx)합니다. 이렇게 하면 네트워크 트래픽을 hello hello 컴퓨터 간에 통신할 수 있습니다. 연결 된 tooeach 컴퓨터 하는 동안 명령 프롬프트를 열고 입력 하 여 hello IP 주소를 가져올 `ipconfig`합니다. Hello IP를 확인할 수 있습니다 또는 hello 리소스 그룹에 대 한 hello 가상 네트워크 리소스를 선택 하 고 각 이러한 컴퓨터에 대해 만든 hello 네트워크 인터페이스를 검사 하 여 hello 포털에서 각 컴퓨터의 주소입니다.
4. Hello Vm의 tooone를 연결 하 고 테스트 ping 할 수 있는 다른 두 개의 Vm을 성공적으로 hello 합니다.
5. Tooone hello Vm의 연결 및 [Windows Server 용 hello 독립 실행형 서비스 패브릭 패키지를 다운로드](http://go.microsoft.com/fwlink/?LinkId=730690) hello에 새 폴더에 컴퓨터와 hello 패키지 압축을 풉니다.
6. 열기 hello *ClusterConfig.Unsecure.MultiMachine.json* 메모장에서 파일을 hello 컴퓨터의 hello 3 IP 주소와 각 노드를 편집 합니다. Hello 위쪽에 hello 클러스터 이름을 변경 하 고 hello 파일을 저장 합니다.  Hello 클러스터 매니페스트의 부분적으로 예는 다음과 같습니다.
   
    ```
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "01-2017",
        "nodes": [
        {
            "nodeName": "standalonenode0",
            "iPAddress": "10.1.0.4",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD0"
        },
        {
            "nodeName": "standalonenode1",
            "iPAddress": "10.1.0.5",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc2/r0",
            "upgradeDomain": "UD1"
        },
        {
            "nodeName": "standalonenode2",
            "iPAddress": "10.1.0.6",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc3/r0",
            "upgradeDomain": "UD2"
        }
        ],
    ```
7. 이 toobe 보안 클러스터를 가져오려는 경우 결정 hello 보안 조치 toouse 선택한 hello 단계 hello에 따라 관련 링크: [X509 인증서](service-fabric-windows-cluster-x509-security.md) 또는 [Windows 보안](service-fabric-windows-cluster-windows-security.md)합니다. Windows 보안을 사용 하 여 hello 클러스터를 설정 하는 경우 도메인 컨트롤러 toomanage Active Directory를 tooset을 해야 합니다. 도메인 컨트롤러 컴퓨터를 Service Fabric 노드로 사용하는 것은 지원되지 않습니다.
8. [PowerShell ISE 창](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise)을 엽니다. Hello 다운로드 한 독립 실행형 설치 관리자 패키지를 추출 하 고 hello 클러스터 구성 파일이 저장 되어 있는 toohello 폴더를 이동 합니다. 다음 PowerShell 명령을 toodeploy hello 클러스터 hello를 실행 합니다.
   
    ```
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.MultiMachine.json
    ```

hello 스크립트 hello 서비스 패브릭 클러스터를 원격으로 구성 됩니다 하 고 배포를 통해 롤업 하는 대로 진행 상황을 보고 해야 합니다.

9. Toohello 연결 하 여 hello 클러스터는 작동 하는 경우 확인 수를 대략 1 분에 한 후 hello 컴퓨터의 IP 중 하나를 사용 하 여 서비스 패브릭 탐색기 주소, 예를 사용 하 여 `http://10.1.0.5:19080/Explorer/index.html`합니다. 

## <a name="next-steps"></a>다음 단계
* [Windows Server 또는 Linux에서 독립 실행형 서비스 패브릭 클러스터 만들기](service-fabric-deploy-anywhere.md)
* [추가 또는 노드 tooa 독립 실행형 서비스 패브릭 클러스터를 제거 합니다.](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [독립 실행형 Windows 클러스터에 대한 구성 설정](service-fabric-cluster-manifest.md)
* [Windows 보안을 사용하여 독립 실행형 클러스터 보호](service-fabric-windows-cluster-windows-security.md)
* [X509 인증서를 사용하여 Windows에서 독립 실행형 클러스터 보호](service-fabric-windows-cluster-x509-security.md)

