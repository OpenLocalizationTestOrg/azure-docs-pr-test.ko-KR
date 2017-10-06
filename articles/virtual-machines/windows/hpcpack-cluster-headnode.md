---
title: "Azure VM에서 HPC Pack 헤드 노드는 aaaCreate | Microsoft Docs"
description: "어떻게 toouse hello Azure 포털 및 hello 리소스 관리자 배포 toocreate Microsoft HPC Pack 2012 R2 헤드 노드를에서 모델링 하는 Azure VM에 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: e6a13eaf-9124-47b4-8d75-2bc4672b8f21
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 3ddefb74b053a48a15f1ba1ca8edbc0192da51a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hello-head-node-of-an-hpc-pack-cluster-in-an-azure-vm-with-a-marketplace-image"></a>마켓플레이스 이미지를 사용 하는 Azure VM에서 HPC Pack 클러스터의 헤드 노드 hello 만들기
사용 하 여 한 [Microsoft HPC Pack 2012 R2 가상 컴퓨터 이미지](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) hello Azure 마켓플레이스와 hello Azure 포털 toocreate hello 헤드 노드에서 HPC 클러스터의 합니다. 이 HPC 팩 VM 이미지는 HPC 팩 2012 R2 업데이트 3이 미리 설치된 Windows Server 2012 R2 Datacenter를 기준으로 합니다. Azure에서 HPC 팩의 개념 증명 배포에 대해 이 헤드 노드를 사용합니다. 다음 계산 노드 toohello 클러스터 toorun HPC 작업을 추가할 수 있습니다.

> [!TIP]
> hello 헤드 노드와 계산 노드를 포함 하는 Azure의 HPC Pack 2012 R2 클러스터 완료 toodeploy 자동화 된 방법을 사용 하는 것이 좋습니다. 옵션 포함 hello [HPC Pack IaaS 배포 스크립트](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) 및 hello와 같은 리소스 관리자 템플릿 [Windows 작업에 대 한 HPC 팩 클러스터](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)합니다. Resource Manager 템플릿은 [Microsoft HPC 팩 2016 클러스터](https://github.com/MsHpcPack/HPCPack2016/tree/master/newcluster-templates)에 사용할 수도 있습니다. 
> 
> 

## <a name="planning-considerations"></a>고려 사항 계획
Hello 다음 그림에에서 나와 있는 것 처럼 Azure 가상 네트워크의 Active Directory 도메인의 hello HPC Pack 헤드 노드를 배포 합니다.

![HPC 팩 헤드 노드][headnode]

* **Active Directory 도메인**: hello 헤드 노드가 있어야 하는 HPC Pack 2012 R2 도메인에 가입 tooan Active Directory Azure의 hello VM에서 hello HPC 서비스를 시작 하기 전에. 개념 배포의 증거에 대 한이 문서에 나와 있는 것 처럼 만드는 VM hello 헤드 노드에 대 한 도메인 컨트롤러로 hello HPC 서비스를 시작 하기 전에 hello를 승격할 수 있습니다. 두 번째 방법은 toodeploy 별도 도메인 컨트롤러 및 Azure toowhich 참여에서 포리스트 hello 헤드 노드 VM입니다.

* **배포 모델**: 대부분의 새 배포에 대 한 hello 리소스 관리자 배포 모델을 사용 하는 것이 좋습니다. 이 문서에서는 배포 모델을 사용하는 것으로 가정합니다.

* **Azure 가상 네트워크**: 지정 hello 리소스 관리자 배포 모델 toodeploy hello 헤드 노드를 사용 하거나 Azure 가상 네트워크를 만듭니다. Toojoin hello 헤드 노드 tooan 기존의 Active Directory 도메인을 사용 해야 할 경우에 hello 가상 네트워크를 사용 합니다. 또한 해야 이후 tooadd 계산 노드 Vm toohello 클러스터.

## <a name="steps-toocreate-hello-head-node"></a>단계 toocreate hello 헤드 노드
다음은 hello 리소스 관리자 배포 모델을 사용 하 여 고급 단계 toouse hello Azure 포털 toocreate hello HPC Pack 헤드 노드 용 Azure VM입니다. 

1. 한 가지 옵션은 toouse toocreate 별도 도메인 컨트롤러 Vm와 Azure에서 새 Active Directory 포리스트를 원하는 경우는 [리소스 관리자 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/active-directory-new-domain-ha-2-dc)합니다. 개념 배포의 간단한 증거에 대 한 있기 tooomit이이 단계를 미세 하 고 hello 헤드 노드 VM 자체를 도메인 컨트롤러로 구성 합니다. 이 옵션은 이 문서의 뒷부분에서 설명합니다.
2. Hello에 [HPC Pack 2012 r 2에서 Windows Server 2012 R2 페이지](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) hello Azure 마켓플레이스, 클릭 **가상 컴퓨터 만들기**합니다. 
3. Hello 포털 hello **Windows Server 2012 r 2에서 HPC Pack 2012 R2** 페이지, 선택 hello **리소스 관리자** 배포 모델 및 클릭 **만들기**합니다.
   
    ![HPC 팩 이미지][marketplace]
4. Hello 포털 tooconfigure hello 설정을 사용 하 고 hello VM을 만듭니다. 새 tooAzure 인 경우 hello 자습서에 따라 [hello Azure 포털에서에서 Windows 가상 컴퓨터를 만들](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. 에 대 한 개념 배포의 증거를 일반적으로 hello 기본 수락 하거나 권장 되는 설정입니다.
   
   > [!NOTE]
   > Azure에서 Active Directory 도메인을 기존 toojoin hello 헤드 노드 tooan 원하는 hello VM을 만들 때 해당 도메인에 대 한 hello 가상 네트워크를 지정 해야 합니다.
   > 
   > 
5. Hello VM 만들고 hello VM이 실행 되 고, [toohello VM 연결](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 원격 데스크톱으로 합니다. 
6. Hello 다음 옵션 중 하나를 선택 하 여 hello VM tooan Active Directory 포리스트를 도메인에 가입 시킵니다.
   
   * Azure 가상 네트워크를 기존 도메인 포리스트에에서 hello VM을 만든 경우 표준 서버 관리자 또는 Windows PowerShell 도구를 사용 하 여 hello VM toohello 포리스트를 조인 합니다. 그런 다음 다시 시작합니다.
   * (하지 않고도 기존 도메인 포리스트가) 새 가상 네트워크에 hello VM을 만든 경우 VM hello 다음 도메인 컨트롤러로 승격 합니다. Tooinstall 표준 단계를 사용 하 고 hello 헤드 노드에서 hello Active Directory 도메인 서비스 역할을 구성 합니다. 자세한 단계를 보려면 [새 Windows Server 2012 Active Directory 포리스트 설치](https://technet.microsoft.com/library/jj574166.aspx)를 참조하세요.
7. Hello 후 VM 실행 중 이며 조인된 tooan Active Directory 포리스트, 다음과 같이 hello HPC 팩 서비스를 시작 합니다.
   
    a. Toohello 헤드 노드 VM hello 로컬 관리자 그룹의 구성원 인 도메인 계정을 사용 하 여 연결 합니다. 예를 들어 hello 헤드 노드 VM을 만들 때 설정 하는 hello 관리자 계정을 사용 합니다.
   
    b. 기본 헤드 노드 구성에 대 한 관리자 권한으로 Windows PowerShell을 시작 하 고 hello 다음 입력:
   
    ```PowerShell
    & $env:CCP_HOME\bin\HPCHNPrepare.ps1 –DBServerInstance ".\ComputeCluster"
    ```
   
    HPC Pack 서비스 toostart hello에 대 일 분 정도 걸릴 수 있습니다.
   
    추가 헤드 노드 구성 옵션을 보려면 `get-help HPCHNPrepare.ps1`을 입력합니다.

## <a name="next-steps"></a>다음 단계
* 이제 hello HPC 팩 클러스터의 헤드 노드를 사용할 수 있습니다. 예를 들어 시작 HPC 클러스터 관리자 및 전체 hello [배포 할 일 목록](https://technet.microsoft.com/library/jj884141.aspx)합니다.
* Tooincrease hello 클러스터 용량 요청 시 계산 추가 [Azure 버스트 노드](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) 클라우드 서비스에 있습니다. 
* Hello 클러스터에서 테스트 작업을 실행 해 보십시오. 예를 들어 hello HPC Pack을 참조 하십시오. [시작 가이드](https://technet.microsoft.com/library/jj884144)합니다.

<!--Image references-->
[headnode]: ./media/hpcpack-cluster-headnode/headnode.png
[marketplace]: ./media/hpcpack-cluster-headnode/marketplace.png
