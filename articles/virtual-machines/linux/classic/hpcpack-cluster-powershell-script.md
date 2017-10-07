---
title: "aaaPowerShell 스크립트 toodeploy Linux HPC 클러스터 | Microsoft Docs"
description: "Azure 가상 컴퓨터에서 PowerShell 스크립트 toodeploy Linux HPC Pack 2012 R2 클러스터를 실행 합니다."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 73041960-58d3-4ecf-9540-d7e1a612c467
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 885b03fa2fd604827dc388803fc21debab730979
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a>Hello HPC Pack IaaS 배포 스크립트와 함께 Linux 고성능 HPC (컴퓨팅) 클러스터 만들기
Azure 가상 컴퓨터의 hello HPC Pack IaaS 배포 PowerShell 스크립트 toodeploy Linux 작업에 대 한 전체 HPC Pack 2012 R2 클러스터를 실행 합니다. hello 클러스터가 HPC Pack에서 지 원하는 Linux 배포 hello 중 하나를 실행 하는 계산 노드 및 Windows Server 및 Microsoft HPC Pack을 실행 하는 Active Directory에 가입 된 헤드 노드 구성 됩니다. Windows Azure에 대 한 작업에서 HPC Pack 클러스터 toodeploy 참조 [hello HPC Pack IaaS 배포 스크립트 사용 Windows HPC 클러스터를 만들고](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다. Azure 리소스 관리자 템플릿 toodeploy HPC Pack 클러스터를 사용할 수 있습니다. 예제는 [Linux 계산 노드가 포함된 HPC 클러스터 만들기](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/)를 참조하세요.

> [!IMPORTANT] 
> 이 문서에 설명 된 PowerShell 스크립트 hello hello 클래식 배포 모델을 사용 하 여 Azure에 Microsoft HPC Pack 2012 R2 클러스터를 만듭니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.
> 또한이 문서에 설명 된 hello 스크립트는 HPC 팩 2016을 지원 하지 않습니다.

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-file"></a>예제 구성 파일
hello 다음 구성 파일을 도메인 컨트롤러 및 도메인 포리스트 만들고 10 Linux 계산 노드 및 로컬 데이터베이스가 있는 헤드 노드 하나에 HPC Pack 클러스터를 배포 합니다. 모든 hello 클라우드 서비스는 hello 동아시아 지역에 직접 생성 됩니다. hello Linux 계산 노드가 생성 되어 두 개의 클라우드 서비스 및 두 개의 저장소 계정에서 (즉, *MyLnxCN 0001* 를 *MyLnxCN 0005* 에 *MyLnxCNService01* 및 *mylnxstorage01*, 및 *MyLnxCN 0006* 를 *MyLnxCN 0010* 에 *MyLnxCNService02* 및 *mylnxstorage02* ). hello 계산 노드가 OpenLogic CentOS 버전 7.0 Linux 이미지에서 만들어집니다. 

구독 이름 및 hello 계정 및 서비스 이름에 대 한 고유한 값으로 대체 합니다.

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>MyDCServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>Large</VMSize>
    </DomainController>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>MyLnxCN-%0001%</VMNamePattern>
    <ServiceNamePattern>MyLnxCNService%01%</ServiceNamePattern>
    <MaxNodeCountPerService>5</MaxNodeCountPerService>
    <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>10</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325 </ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```
## <a name="troubleshooting"></a>문제 해결
* **"VNet이 없음" 오류**. 하나 이상의 배포를 실행 하면 hello HPC Pack IaaS 배포 스크립트 toodeploy 여러 클러스터 Azure에서 동시에 하나의 구독으로 hello 오류가 발생할 수 있습니다 "VNet *VNet\_이름* 존재 하지 않는"입니다.
  이 오류가 발생 하면 실패 하는 hello 배포에 대 한 hello 스크립트를 다시 실행 합니다.
* **Hello Azure 가상 네트워크에서에서 인터넷 hello 문제 액세스**합니다. 헤드 노드 VM toodomain 컨트롤러를 수동으로 승격 이나 hello 배포 스크립트를 사용 하 여 새 도메인 컨트롤러와 HPC Pack 클러스터를 만들 때, hello Vm hello Azure 가상 네트워크 toohello 인터넷에에서 연결할 때 문제가 발생할 수 있습니다. 이 전달자 DNS 서버가 hello 도메인 컨트롤러에서 자동으로 구성 되 고이 전달자 DNS 서버가 제대로 확인 되지 않습니다 하는 경우에 발생할 수 있습니다.
  
    이 문제를 해결 toowork toohello 도메인 컨트롤러와 제거 hello 전달자 구성 설정 하거나 로그온 하거나 유효한 전달자 DNS 서버를 구성 합니다. 서버 관리자에서이 클릭 toodo **도구** > **DNS** tooopen DNS 관리자를 두 번 클릭 하 고 **전달자**합니다.

## <a name="next-steps"></a>다음 단계
* 참조 [Azure에서 HPC Pack 클러스터에서 계산 노드 Linux 시작](hpcpack-cluster.md) 지원 되는 Linux 배포판에 대 한 내용은 데이터를 이동 하 고 Linux로 tooan HPC Pack 클러스터 작업을 제출 하는 계산 노드.
* Hello 스크립트 toocreate 클러스터를 사용 하 고 Linux HPC 작업을 실행 하는 자습서를 보려면
  * [Azure의 Linux 계산 노드에서 Microsoft HPC 팩을 사용하여 NAMD 실행](hpcpack-cluster-namd.md)
  * [Azure의 Linux 계산 노드에서 Microsoft HPC 팩을 사용하여 OpenFOAM 실행](hpcpack-cluster-openfoam.md)
  * [Azure의 Linux 계산 노드에서 Microsoft HPC 팩을 사용하여 STAR-CCM+ 실행](hpcpack-cluster-starccm.md)

