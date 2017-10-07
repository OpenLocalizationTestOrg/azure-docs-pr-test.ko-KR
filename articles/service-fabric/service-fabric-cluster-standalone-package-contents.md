---
title: "Windows Server 용 서비스 패브릭 독립 실행형 패키지 aaaAzure | Microsoft Docs"
description: "설명 및 Windows Server 용 hello Azure 서비스 패브릭 독립 실행형 패키지 내용의 압축 합니다."
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
ms.date: 8/10/2017
ms.author: chackdan;maburlik
ms.openlocfilehash: e4c6cb9128d659144e559fcad06bb78c9969dd60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="contents-of-service-fabric-standalone-package-for-windows-server"></a>Windows Server용 Service Fabric 독립 실행형 패키지의 내용
Hello에 [다운로드](http://go.microsoft.com/fwlink/?LinkId=730690) 서비스 패브릭 독립 실행형 패키지 파일을 다음 hello를 찾을 수 있습니다.

| **파일 이름** | **간단한 설명** |
| --- | --- |
| CreateServiceFabricCluster.ps1 |PowerShell 스크립트를 ClusterConfig.json에 hello 설정을 사용 하 여 hello 클러스터를 만듭니다. |
| RemoveServiceFabricCluster.ps1 |ClusterConfig.json에 hello 설정을 사용 하 여 클러스터를 제거 하는 PowerShell 스크립트입니다. |
| AddNode.ps1 |기존 노드 tooan 추가 대 한 PowerShell 스크립트 hello 현재 컴퓨터에서 클러스터를 배포 합니다. |
| RemoveNode.ps1 |기존 노드를 제거 하기 위한 PowerShell 스크립트는 hello 현재 컴퓨터에서 클러스터를 배포 합니다. |
| CleanFabric.ps1 |독립 실행형 서비스 패브릭 설치 hello 현재 컴퓨터의 전원을 정리 하기 위해 PowerShell 스크립트입니다. 이전 MSI 설치는 자체 연결된 제거 프로그램을 사용하여 제거됩니다. |
| TestConfiguration.ps1 |Hello Cluster.json에에서 지정 된 대로 hello 인프라를 분석 하기 위한 PowerShell 스크립트입니다. |
| DownloadServiceFabricRuntimePackage.ps1 |Hello 컴퓨터를 배포 하지 않은 시나리오 toohello 연결에 대 한 대역 외, hello 최신 런타임 패키지의 다운로드에 사용 되는 PowerShell 스크립트 인터넷 합니다. |
| DeploymentComponentsAutoextractor.exe |자동 배포 구성 요소를 포함 하는 보관 파일 압축 풀기 사용 되는 hello에서 독립 실행형 패키지 스크립트입니다. |
| EULA_ENU.txt |hello 사용 약관 hello에 대 한 Microsoft Azure 서비스 패브릭 독립 실행형 Windows Server 패키지를 활용합니다. 있습니다 수 [hello EULA 복사본을 다운로드](http://go.microsoft.com/fwlink/?LinkID=733084) 이제 합니다. |
| Readme.txt |링크 toohello 릴리스 정보 및 기본 설치 지침이 나와 있습니다. 이 문서에 hello 지침의 하위 집합은 |
| ThirdPartyNotice.rtf |Hello 패키지에 있는 타사 소프트웨어를 확인 합니다. |
| Tools\Microsoft.Azure.ServiceFabric.WindowsServer.SupportPackage.zip |필요 시 toocollect 및 업로드 추적에서 실행 되는 StandaloneLogCollector.exe tooMicrosoft 지원 목적을 위해를 기록 합니다. |
| Tools\ServiceFabricUpdateService.zip |인터넷 권한이 있는 클러스터에 tooenable 자동 코드 업그레이드를 사용 하는 도구입니다. 자세한 내용은 [여기](service-fabric-cluster-upgrade-windows-server.md)|

**템플릿** 
| **파일 이름** | **간단한 설명** |
| --- | --- |
| ClusterConfig.Unsecure.DevCluster.json |보안 되지 않은, 3 노드 단일 컴퓨터 (또는 가상 컴퓨터) 개발 클러스터의 경우 hello 클러스터의 각 노드에 대 한 hello 정보를 포함 하 여 hello 설정을 포함 하는 클러스터 구성 샘플 파일입니다. |
| ClusterConfig.Unsecure.MultiMachine.json |Hello 클러스터의 각 컴퓨터에 대 한 hello 정보를 포함 하는 보안 되지 않은, 다중 컴퓨터 (또는 가상 컴퓨터) 클러스터에 대 한 hello 설정을 포함 하는 클러스터 구성 샘플 파일입니다. |
| ClusterConfig.Windows.DevCluster.json |Hello 클러스터에 속한 각 노드에 대 한 hello 정보를 포함 하 여 hello 3 노드를 안전 하 고 단일 컴퓨터 (또는 가상 컴퓨터)에 대 한 설정을 개발 클러스터를 모두 포함 하는 클러스터 구성 샘플 파일입니다. 사용 하 여 hello 클러스터는 보안 [Windows id](https://msdn.microsoft.com/library/ff649396.aspx)합니다. |
| ClusterConfig.Windows.MultiMachine.json |Hello 보안 클러스터에 속한 각 컴퓨터에 대 한 hello 정보를 비롯 한 Windows 보안을 사용 하는 안전한 다중 컴퓨터 (또는 가상 컴퓨터) 클러스터에 대 한 모든 hello 설정을 포함 하는 클러스터 구성 샘플 파일입니다. 사용 하 여 hello 클러스터는 보안 [Windows id](https://msdn.microsoft.com/library/ff649396.aspx)합니다. |
| ClusterConfig.x509.DevCluster.json |3 노드를 안전 하 고 단일 컴퓨터 (또는 가상 컴퓨터) 개발 클러스터에 대해 hello 클러스터의 각 노드에 대 한 hello 정보를 포함 하 여 모든 hello 설정을 포함 하는 클러스터 구성 샘플 파일입니다. hello 클러스터로 보호 될 x509 인증서입니다. |
| ClusterConfig.x509.MultiMachine.json |Hello에 대 한 모든 hello 설정을 포함 하는 클러스터 구성 샘플 파일 안전 하 게 hello 보안 클러스터의 각 노드에 대 한 hello 정보를 포함 하는 클러스터 다중 컴퓨터 (또는 가상 컴퓨터). hello 클러스터로 보호 될 x509 인증서입니다. |
| ClusterConfig.gMSA.Windows.MultiMachine.json |Hello에 대 한 모든 hello 설정을 포함 하는 클러스터 구성 샘플 파일 안전 하 게 hello 보안 클러스터의 각 노드에 대 한 hello 정보를 포함 하는 클러스터 다중 컴퓨터 (또는 가상 컴퓨터). hello 클러스터로 보호 될 [그룹 관리 서비스 계정](https://technet.microsoft.com/en-us/library/jj128431(v=ws.11).aspx)합니다. |

## <a name="cluster-configuration-samples"></a>클러스터 구성 샘플
Hello GitHub 페이지에서 클러스터 구성에 대 한 템플릿의 최신 버전을 찾을 수 있습니다: [독립 실행형 클러스터 구성 예제](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)합니다.

## <a name="independent-runtime-package"></a>독립 런타임 패키지
클러스터 배포 시 hello 최신 런타임 패키지를 자동으로 다운로드 [다운로드 링크-서비스 패브릭 런타임을-Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)합니다.

## <a name="related"></a>관련 항목
* [독립 실행형 Azure Service Fabric 클러스터 만들기](service-fabric-cluster-creation-for-windows-server.md)
* [Service Fabric 클러스터 보안 시나리오](service-fabric-windows-cluster-windows-security.md)
