---
title: "aaaPowerShell 스크립트 toodeploy Windows HPC 클러스터 | Microsoft Docs"
description: "Azure 가상 컴퓨터에서 PowerShell 스크립트 toodeploy Windows HPC Pack 2012 R2 클러스터를 실행 합니다."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 286b2be8-2533-40df-b02a-26156b1f1133
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 10ce1e9bc4e98954b955549bd72aaaf6106c69fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a>Hello HPC Pack IaaS 배포 스크립트와 함께 Windows 고성능 HPC (컴퓨팅) 클러스터 만들기
Azure 가상 컴퓨터의 hello HPC Pack IaaS 배포 PowerShell 스크립트 toodeploy Windows 작업에 대 한 전체 HPC Pack 2012 R2 클러스터를 실행 합니다. 추가 창 계산 지정한 리소스 및 Windows Server 및 Microsoft HPC Pack을 실행 하는 Active Directory에 가입 된 헤드 노드 hello 클러스터 구성 됩니다. Azure에서 HPC Pack 클러스터 toodeploy Linux 작업에 대 한 경우 참조 [HPC Pack IaaS 배포 스크립트 hello로 Linux HPC 클러스터 만들기](../../linux/classic/hpcpack-cluster-powershell-script.md)합니다. Azure 리소스 관리자 템플릿 toodeploy HPC Pack 클러스터를 사용할 수 있습니다. 예제는 [HPC 클러스터 만들기](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) 및 [사용자 지정 계산 노드 이미지로 HPC 클러스터 만들기](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/)를 참조하세요.

> [!IMPORTANT] 
> 이 문서에 설명 된 PowerShell 스크립트 hello hello 클래식 배포 모델을 사용 하 여 Azure에 Microsoft HPC Pack 2012 R2 클러스터를 만듭니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.
> 또한이 문서에 설명 된 hello 스크립트는 HPC 팩 2016을 지원 하지 않습니다.

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-files"></a>예제 구성 파일
Hello 다음 예제에서는 사용자 고유의 구독 Id에 대 한 값 또는 이름 및 hello 계정 및 서비스 이름을 대체 합니다.

### <a name="example-1"></a>예 1
hello 다음 구성 파일 배포 로컬 데이터베이스가 있는 헤드 노드 및 hello Windows Server 2012 R2 운영 체제를 실행 하는 5 개의 계산 노드가 있는 HPC Pack 클러스터 됩니다. 모든 hello 클라우드 서비스는 hello West US 위치에 직접 생성 됩니다. 헤드 노드 hello hello 도메인 포리스트의 도메인 컨트롤러 역할을 합니다.

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionId>08701940-C02E-452F-B0B1-39D50119F267</SubscriptionId>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%1000%</VMNamePattern>
    <ServiceName>MyHPCCNService</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>5</NodeCount>
    <OSVersion>WindowsServer2012R2</OSVersion>
  </ComputeNodes>
</IaaSClusterConfig>
```

### <a name="example-2"></a>예 2
다음 구성 파일 hello 기존 도메인 포리스트에 HPC Pack 클러스터를 배포 합니다. hello 클러스터에 로컬 데이터베이스가 있는 헤드 노드 1 및 계산 노드 VM BGInfo 확장이 적용 hello로 12입니다.
Windows 업데이트 자동 설치는 모든 hello hello 도메인 포리스트에 Vm에 대 한 비활성화 됩니다. 모든 hello 클라우드 서비스는 동아시아 지역에 직접 생성 됩니다. hello 계산 노드는 3 개의 클라우드 서비스 및 3 개 저장소 계정에서 생성 됩니다: *MyHPCCN 0001* 너무*MyHPCCN 0005* 에 *MyHPCCNService01* 및  *mycnstorage01*; *MyHPCCN 0006* 너무*MyHPCCN0010* 에 *MyHPCCNService02* 및 *mycnstorage02*; 및  *MyHPCCN-0011* 너무*MyHPCCN 0012* 에 *MyHPCCNService03* 및 *mycnstorage03*). hello 계산 노드가 계산 노드에서 캡처된 기존 개인 이미지에서 만들어집니다. hello 자동 확장 및 축소 이며 기본값은 서비스를 사용 하는 확장 및 간격을 축소 합니다.

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
     <NoWindowsAutoUpdate />
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <Certificates>
    <Certificate>
      <Id>1</Id>
      <PfxFile>d:\mytestcert1.pfx</PfxFile>
      <Password>MyPsw!!2</Password>
    </Certificate>
  </Certificates>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%0001%</VMNamePattern>
<ServiceNamePattern>MyHPCCNService%01%</ServiceNamePattern>
<MaxNodeCountPerService>5</MaxNodeCountPerService>
<StorageAccountNamePattern>mycnstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>12</NodeCount>
    <ImageName HPCPackInstalled=”true”>MyHPCComputeNodeImage</ImageName>
    <VMExtensions>
       <VMExtension>
          <ExtensionName>BGInfo</ExtensionName>
          <Publisher>Microsoft.Compute</Publisher>
          <Version>1.*</Version>
       </VMExtension>
    </VMExtensions>
  </ComputeNodes>
  <AutoGrowShrink>
    <CertificateId>1</CertificateId>
  </AutoGrowShrink>
</IaaSClusterConfig>

```

### <a name="example-3"></a>예 3
다음 구성 파일 hello 기존 도메인 포리스트에 HPC Pack 클러스터를 배포 합니다. hello 클러스터 hello Windows Server 2012 R2 운영 체제 및 hello Windows Server 2012 R2 운영 체제를 실행 하는 5 개의 계산 노드를 실행 하는 두 개의 브로커 노드 하나 헤드 노드, 500GB 데이터 디스크와 데이터베이스 서버를 하나 포함 됩니다. 클라우드 서비스 MyHPCCNService hello 선호도 그룹에서 생성 된 hello *MyIBAffinityGroup*, hello 다른 클라우드 서비스에서에서 만들어진 hello 선호도 그룹 및 *MyAffinityGroup*합니다. hello HPC 작업 스케줄러 REST API 및 HPC 웹 포털은 헤드 노드 hello에 활성화 됩니다.

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <AffinityGroup>MyAffinityGroup</AffinityGroup>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>    
  <Domain>
    <DCOption>ExistingDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>NewRemoteDB</DBOption>
    <DBVersion>SQLServer2014_Enterprise</DBVersion>
    <DBServer>
      <VMName>MyDBServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>ExtraLarge</VMSize>
      <DataDiskSizeInGB>500</DataDiskSizeInGB>
    </DBServer>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%0000%</VMNamePattern>
    <ServiceName>MyHPCCNService</ServiceName>
    <VMSize>A8</VMSize>
<NodeCount>5</NodeCount>
<AffinityGroup>MyIBAffinityGroup</AffinityGroup>
  </ComputeNodes>
  <BrokerNodes>
    <VMNamePattern>MyHPCBN-%0000%</VMNamePattern>
    <ServiceName>MyHPCBNService</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>2</NodeCount>
  </BrokerNodes>
</IaaSClusterConfig>
```



### <a name="example-4"></a>예제 4
다음 구성 파일 hello 기존 도메인 포리스트에 HPC Pack 클러스터를 배포 합니다. hello 클러스터에 로컬 데이터베이스가 있는 헤드 노드를 두 개, 두 개의 Azure 노드 템플릿을 만들고 Azure 노드 템플릿에 대 한 세 가지 크기 보통 Azure 노드가 만들어집니다 *AzureTemplate1*합니다. Hello 헤드 노드를 구성한 후 hello 헤드 노드에서 스크립트 파일을 실행 합니다.

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <AffinityGroup>MyAffinityGroup</AffinityGroup>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>ExistingDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
<VMSize>ExtraLarge</VMSize>
    <PostConfigScript>c:\MyHNPostActions.ps1</PostConfigScript>
  </HeadNode>
  <Certificates>
    <Certificate>
      <Id>1</Id>
      <PfxFile>d:\mytestcert1.pfx</PfxFile>
      <Password>MyPsw!!2</Password>
    </Certificate>
    <Certificate>
      <Id>2</Id>
      <PfxFile>d:\mytestcert2.pfx</PfxFile>
    </Certificate>    
  </Certificates>
  <AzureBurst>
    <AzureNodeTemplate>
      <TemplateName>AzureTemplate1</TemplateName>
      <SubscriptionId>bb9252ba-831f-4c9d-ae14-9a38e6da8ee4</SubscriptionId>
      <CertificateId>1</CertificateId>
      <ServiceName>mytestsvc1</ServiceName>
      <StorageAccount>myteststorage1</StorageAccount>
      <NodeCount>3</NodeCount>
      <RoleSize>Medium</RoleSize>
    </AzureNodeTemplate>
    <AzureNodeTemplate>
      <TemplateName>AzureTemplate2</TemplateName>
      <SubscriptionId>ad4b9f9f-05f2-4c74-a83f-f2eb73000e0b</SubscriptionId>
      <CertificateId>1</CertificateId>
      <ServiceName>mytestsvc2</ServiceName>
      <StorageAccount>myteststorage2</StorageAccount>
      <Proxy>
        <UsesStaticProxyCount>false</UsesStaticProxyCount>     
        <ProxyRatio>100</ProxyRatio>
        <ProxyRatioBase>400</ProxyRatioBase>
      </Proxy>
      <OSVersion>WindowsServer2012</OSVersion>
    </AzureNodeTemplate>
  </AzureBurst>
</IaaSClusterConfig>
```

## <a name="troubleshooting"></a>문제 해결
* **"VNet 존재 하지 않습니다." 오류** -하나 이상의 배포를 실행 하면 hello 스크립트 toodeploy 여러 클러스터 Azure에서 동시에 하나의 구독으로 hello 오류가 발생할 수 있습니다 "VNet *VNet\_이름* 하지 않습니다 "존재 합니다.
  이 오류가 발생 하면 실패 하는 hello 배포에 대 한 다시 hello 스크립트를 실행 합니다.
* **Hello Azure 가상 네트워크에서에서 인터넷 hello 문제 액세스** -hello 배포 스크립트를 사용 하 여 새 도메인 컨트롤러를 가진 클러스터를 만들 또는 수동으로 헤드 노드 VM toodomain 컨트롤러를 승격 하 고, 문제가 발생할 수 있습니다 하는 경우 hello Vm toohello 인터넷 연결을 연결합니다. 이 문제는 전달자 DNS 서버가 hello 도메인 컨트롤러에서 자동으로 구성 되 고이 전달자 DNS 서버가 제대로 확인 되지 않습니다 발생할 수 있습니다.
  
    이 문제를 해결 toowork toohello 도메인 컨트롤러와 제거 hello 전달자 구성 설정 하거나 로그온 하거나 유효한 전달자 DNS 서버를 구성 합니다. 서버 관리자에서이 설정을 클릭 tooconfigure **도구** >
    **DNS** tooopen DNS 관리자를 두 번 클릭 하 고 **전달자**합니다.
* **계산 집약적인 Vm에서 RDMA 네트워크에 액세스 하는 문제** -Windows Server 계산을 추가 또는 A8 또는 A9 등 브로커 노드는 RDMA 가능을 사용 하 여 Vm 크기, 이러한 Vm toohello RDMA 응용 프로그램 네트워크 연결 문제가 발생할 수 있습니다 하는 경우. 이 문제가 발생 하는 한 가지 이유는 경우 hello HpcVmDrivers 확장이 제대로 설치 되지 않았습니다 hello Vm이 toohello 클러스터를 추가 하는 경우. 예를 들어 확장 상태를 설치 하는 hello 멈춰 있을 수 있습니다.
  
    toowork 첫 번째 hello Vm에서 hello 확장의 hello 상태 확인이이 문제를 해결 합니다. Hello 확장이 제대로 설치 되지 않은 경우 hello 노드 hello HPC 클러스터에서 제거를 시도 하 고 hello 노드를 다시 추가 하십시오. 예를 들어 hello 헤드 노드에서 hello Add-hpciaasnode.ps1 스크립트를 실행 하 여 계산 노드 Vm을 추가할 수 있습니다.

## <a name="next-steps"></a>다음 단계
* Hello 클러스터에서 테스트 작업을 실행 해 보십시오. 예를 들어 hello HPC Pack을 참조 하십시오. [시작 가이드](https://technet.microsoft.com/library/jj884144)합니다.
* 자습서 tooscript hello 클러스터 배포를 실행 하는 HPC 작업에 대 한 참조 [Azure toorun Excel 및 SOA 작업에서 HPC Pack 클러스터 시작](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.
* HPC Pack 도구 toostart 시도, 중지, 추가 및 만들면 클러스터에서 계산 노드를 제거 합니다. [Azure에서 HPC Pack 클러스터의 계산 노드 관리](hpcpack-cluster-node-manage.md)를 참조하세요.
* 로컬 컴퓨터에서 toosubmit 작업 toohello 클러스터를 설정 하는 tooget 참조 [제출 HPC 작업은 온-프레미스 컴퓨터 tooan HPC Pack에서에서 Azure에 있는 클러스터](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

