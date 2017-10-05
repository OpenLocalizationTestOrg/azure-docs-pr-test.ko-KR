---
title: "클라우드의 Windows HPC 팩 클러스터 옵션 | Microsoft Docs"
description: "Microsoft HPC Pack을 사용하여 Azure 클라우드에서 Windows HPC(고성능 컴퓨팅) 클러스터를 만들고 관리하기 위한 옵션에 대해 알아봅니다."
services: virtual-machines-windows,cloud-services,batch
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 02c5566d-2129-483c-9ecf-0d61030442d7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/06/2017
ms.author: danlep
ms.openlocfilehash: 96a5520d8440af7d8a880c2675a5d4eb4121e9ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="options-with-hpc-pack-to-create-and-manage-a-windows-hpc-cluster-in-azure"></a>HPC Pack을 사용하여 Azure에서 Windows HPC 클러스터를 만들고 관리하기 위한 옵션
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

이 문서는 Windows 워크로드를 실행하기 위한 HPC Pack 클러스터를 생성하는 옵션을 중점적으로 설명합니다. 또한 [Linux HPC 워크로드](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 실행하는 HPC 팩 클러스터를 생성하는 옵션도 있습니다.


## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a>Azure VM에서 HPC Pack 클러스터 실행
### <a name="azure-templates"></a>Azure 템플릿
* (GitHub) [HPC 팩 2016 클러스터 템플릿](https://github.com/MsHpcPack/HPCPack2016)
* (마켓플레이스) [Windows 워크로드용 HPC 팩 클러스터](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)
* (마켓플레이스) [Excel 워크로드용 HPC 팩 클러스터](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)
* (퀵 스타트) [HPC 클러스터 만들기](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)
* (퀵 스타트) [사용자 지정 계산 노드 이미지로 HPC 클러스터 만들기](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)

### <a name="azure-vm-images"></a>Azure VM 이미지
* [Windows Server 2016의 HPC Pack 2016 헤드 노드](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2016?tab=Overview)
* [Windows Server 2016의 HPC Pack 2016 계산 노드](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2016?tab=Overview)
* [Windows Server 2012 R2의 HPC Pack 2016 헤드 노드](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2012R2?tab=Overview)
* [Windows Server 2012 R2의 HPC Pack 2016 계산 노드](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2012R2?tab=Overview)
* [Windows Server 2012 R2의 HPC Pack 2012 R2 헤드 노드](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)
* [Windows Server 2012 R2의 HPC Pack 2012 R2 계산 노드](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodeonwindowsserver2012r2/)
* [HPC Pack compute node with Excel on Windows Server 2012 R2(영문)](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodewithexcelonwindowsserver2012r2/)

### <a name="powershell-deployment-script"></a>PowerShell 배포 스크립트
* [HPC 팩 IaaS 배포 스크립트를 사용하여 HPC 클러스터 만들기](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="tutorials"></a>자습서
* [자습서: Azure에서 HPC 팩 2016 클러스터 배포](hpcpack-2016-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [자습서: Azure에서 Excel 및 SOA 워크로드를 실행할 HPC 팩 클러스터 시작](excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="manual-deployment-with-the-azure-portal"></a>Azure 포털을 사용하여 수동 배포
* [Azure VM에서 HPC 팩 클러스터의 헤드 노드 설정](hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="cluster-management"></a>클러스터 관리
* [Azure에서 HPC 팩 클러스터의 컴퓨터 노드 관리](classic/hpcpack-cluster-node-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [HPC 팩 클러스터에서 Azure 계산 리소스 확장 및 축소](classic/hpcpack-cluster-node-autogrowshrink.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Azure에서 HPC 팩 클러스터에 작업 제출](hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [HPC Pack의 작업 관리](https://technet.microsoft.com/library/jj899585.aspx)
* [Azure Active Directory로 Azure에서 HPC 팩 클러스터 관리](hpcpack-cluster-active-directory.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="add-worker-role-nodes-to-an-hpc-pack-cluster"></a>HPC Pack 클러스터에 작업자 역할 노드 추가
* [HPC 팩을 사용한 Azure 작업자 인스턴스에 버스트](https://technet.microsoft.com/library/gg481749.aspx)
* [자습서: Azure에서 HPC 팩을 사용하여 하이브리드 클러스터 설정](../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)
* [Azure에서 HPC 팩 헤드 노드에 Azure "버스트" 노드 추가](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="integrate-with-azure-batch"></a>Azure 배치와의 통합
* [HPC 팩을 사용하여 Azure 배치로 버스트](https://technet.microsoft.com/library/mt612877.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a>MPI 작업에 대한 RDMA 클러스터 만들기
* [MPI 응용 프로그램을 실행하기 위해 HPC Pack을 사용하여 Windows RDMA 클러스터 설정](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

