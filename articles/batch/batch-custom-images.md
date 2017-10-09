---
title: "사용자 지정 이미지에서 aaaProvision Azure 배치 풀 | Microsoft Docs"
description: "사용자 지정 이미지 tooprovision 풀 계산 hello 소프트웨어를 포함 하는 노드 및 응용 프로그램에 필요한 데이터를 일괄 처리를 만들 수 있습니다. 사용자 지정 이미지는 tooconfigure 노드 toorun 일괄 처리 작업을 계산 하는 효율적인 방법입니다."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: article
ms.date: 08/07/2017
ms.author: tamram
ms.openlocfilehash: 5cb698ee90f7d3ec9ffe69fa4dc602132c3f7569
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-custom-image-toocreate-a-pool-of-virtual-machines"></a>사용자 지정 이미지 toocreate 가상 컴퓨터의 풀을 사용 하 여

Azure 일괄 처리에서 가상 컴퓨터의 풀을 만들 때 hello 풀의 각 계산 노드에 대 한 hello 운영 체제를 제공 하는 가상 컴퓨터 (VM) 이미지를 지정 합니다. Azure Marketplace 이미지를 사용하거나 사용자가 준비한 사용자 지정 VHD 이미지를 제공하여 가상 컴퓨터 풀을 만들 수 있습니다. 사용자 지정 이미지를 제공 하는 경우 각 계산 노드가 프로 비전 된 hello 시 hello 운영 체제 구성 방법에 대 한 제어를 해야 합니다. Hello에서 사용할 수 있는 참조 데이터는 프로 비전 되는 즉시 계산 노드 및 응용 프로그램 사용자 지정 이미지 포함할 수도 있습니다.

사용자 지정 이미지를 사용 하 여 수 풀의 계산 노드를 가져올 수 있는 시간을 절약할 준비 toorun 일괄 처리 작업 합니다. 프로비전된 후에는 항상 Azure Marketplace 이미지를 사용하고 각 계산 노드에 소프트웨어를 설치할 수 있지만, 이러한 접근 방식은 사용자 지정 이미지를 사용하는 것보다 효율성이 떨어질 수 있습니다. 

몇 가지 이유로 toouse 시나리오에 대해 구성 된 사용자 지정 이미지를 포함할 필요가 없습니다.

- **Hello 운영 체제 (OS) 구성** hello 운영 체제의 특별 한 구성 hello 사용자 지정 이미지에서 수행할 수 있습니다. 
- **대규모 응용 프로그램 설치.** 사용자 지정 이미지에 응용 프로그램을 설치하는 것이 프로비전 후 각 계산 노드에서 설치하는 것보다 더 효율적입니다.
- **많은 양의 데이터 복사.** Hello 데이터 복사 toohello 사용자 지정 이미지를 한 번, 시간 및 대역폭을 절감할 tooeach 계산 노드를 하는 대신 복사 toobe만 필요 합니다.
- **Hello 설치 프로세스 중 hello VM 다시 부팅 합니다.** 재부팅 중 이어서 hello VM 계산 노드 수 있는 경우에 특히 많이 걸릴 수 있습니다.

## <a name="prerequisites"></a>필수 조건

- **Hello 사용자 구독 풀 할당 모드를 사용 하 여 만든 일괄 처리 계정입니다.** toouse 사용자 지정 이미지 tooprovision 가상 컴퓨터 풀을 일괄 처리 계정을 사용자 구독 hello로 만든 [풀 할당 모드](batch-api-basics.md#pool-allocation-mode)합니다. 이 모드에서 일괄 처리 풀 hello 계정이 있는 hello 구독에 할당 됩니다. Hello 참조 [계정](batch-api-basics.md#account) 섹션 [개발 대규모 병렬 일괄 처리를 사용 하 여 솔루션을 계산](batch-api-basics.md) 일괄 처리 계정을 만들 때 hello 풀 할당 모드 설정에 대 한 내용은 합니다.

- **Azure Storage 계정.** 사용자 지정 이미지를 사용 하 여 가상 컴퓨터의 풀 toocreate 해야 hello의 표준, 범용 Azure 저장소 계정 구독 및 지역이 동일한 합니다. Azure VM에서 사용자 지정 이미지를 만드는 경우 다음 복사할 hello 이미지 toohello 저장소 계정이 있는 hello VM의 OS 디스크 있고, 별도 저장소 계정 toocreate 필요 하지는 않습니다. 
    
## <a name="prepare-a-custom-image"></a>사용자 지정 이미지 준비

일괄 처리와 함께 사용할 사용자 지정 이미지 tooprepare Linux 또는 Windows의 기존 설치를 일반화 해야 합니다. 운영 체제 설치를 일반화하면 컴퓨터 특정 정보가 제거되며, hello 결과 다른 컴퓨터 또는 Vm에 설치할 수 있는 이미지입니다.  

> [!IMPORTANT]
> 일괄 처리 Azure를 사용 하 여 현재 지원 하지 않는 이미지 tooprovision 풀을 관리 합니다. hello 사용자 지정 이미지에서는 tooprovision 풀을 Azure 저장소에 저장 해야 합니다. 
>
> 사용자 지정 이미지를 준비할 때는 유의 hello 지점 다음에 유의 하십시오.
> - 일괄 처리 풀 않습니다 tooprovision를 사용 하 여 해당 hello 기본 OS 이미지를 확인 하지는 모든 사전 설치 된 hello 사용자 지정 스크립트 확장 등의 Azure 확장입니다. 사전 설치 된 확장을 포함 하는 hello 이미지를 Azure hello VM을 배포 하는 문제가 발생할 수 있습니다.
> - 제공한 사용 하 여 기본 임시 드라이브 hello hello 배치 노드 에이전트 현재에서는 hello 기본 임시 드라이브 처럼 해당 hello 기본 OS 이미지를 확인 합니다.
>
>

모든 기존의 준비된 Windows 또는 Linux 이미지를 사용자 지정 이미지로 사용할 수 있습니다. 원하는 toouse 로컬 이미지에 대 한 다음 업로드 hello 이미지 tooan Azure 저장소 계정에 있는 경우 동일한 구독 및 지역이 사용 하 여 일괄 처리 계정을 hello 하는 예를 들어 [AzCopy](../storage/storage-use-azcopy.md) 또는 다른 업로드 도구입니다.

새로운 또는 기존 Azure VM에서 사용자 지정 이미지를 준비할 수도 있습니다. 새 VM을 만드는 경우 Azure 마켓플레이스 이미지를 사용자 지정 이미지 hello 기본 이미지로 사용할 수 있으며 사용자 지정 하십시오. toocustomize hello 기본 이미지를 Azure VM을 만들고 응용 프로그램 또는 데이터 tooit를 추가 합니다. 그런 다음 hello VM tooserve로 사용자 지정 이미지를 일반화 하 고 저장소 tooAzure 저장 합니다. 

사용자 지정 이미지를 Azure VM에서 tooprepare 다음이 단계를 따르십시오.

1. Azure Marketplace 이미지에서 **관리되지 않는** Azure VM을 만듭니다. Azure Marketplace에는 [Windows](../virtual-machines/windows/quick-create-portal.md) 및 [Linux](../virtual-machines/linux/quick-create-portal.md) 모두에 대한 이미지가 포함됩니다.
    
    Hello VM 만들기 프로세스의 3 단계에서 선택 했는지 확인 **아니요** 에 대 한 **저장소: 관리 되는 디스크 사용** 옵션입니다. 또한 hello 저장소 계정 이름을 기록해 hello VM의 OS 디스크에 대 한이 저장소 계정은도 Azure 사용자 지정 이미지를 저장 합니다.

    ![관리 되지 않는 VM 및 참고 hello 저장소 계정 이름 만들기](media/batch-custom-images/vm-create-storage.png)
 
2. VM을 만드는 hello 프로세스를 완료 하 고 기다립니다 toobe Azure에서 할당 합니다. 다음은 hello hello 실행 중인 상태에서에서 Azure 포털에서에서 VM을 표시 하는 이미지가입니다.

    ![마켓플레이스 이미지에서 VM 만들기](media/batch-custom-images/vm-status-running.png)

3. Hello VM이 실행 되 면 tooit Windows 용 RDP 또는 SSH (Linux 용)를 통해 연결 합니다. 필요한 소프트웨어를 설치 하거나 원하는 데이터를 복사한 hello VM을 일반화 한 다음 합니다. 에 설명 된 hello 단계에 따라 [VM 일반화 hello](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sa-copy-generalized.md#generalize-the-vm)합니다. 
   
4. 다음과 같이 hello 너무[tooAzure PowerShell 로그인](../virtual-machines/windows/sa-copy-generalized.md#log-in-to-azure-powershell)합니다. Azure PowerShell tooinstall 참조 [Azure PowerShell 개요](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.2.0)합니다. 

5. 다음 너무 hello 단계에 따라[Deallocate hello VM 및 집합 hello 상태 toogeneralized](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sa-copy-generalized#deallocate-the-vm-and-set-the-state-to-generalized)합니다. 

    Hello Azure 포털에서에서 해당 hello VM 할당 취소를 확인 합니다.

    ![해당 hello VM 할당 취소를 확인 합니다.](media/batch-custom-images/vm-status-deallocated.png)

6.  만들기 및 저장 hello VM 이미지 tooAzure 저장소 hello를 사용 하 여 [저장 AzureRmVMImage](https://docs.microsoft.com/powershell/module/azurerm.compute/save-azurermvmimage) PowerShell cmdlet. 에 설명 된 hello 지침에 따라 [hello 이미지 만들기](../virtual-machines/windows/sa-copy-generalized.md#create-the-image)합니다.
    
    hello VM 이미지에는이 절차의 1 단계에서와 같이 hello VM을 만들 때 만든 toohello Azure 저장소 계정을 저장 됩니다. hello 저장 AzureRmVMImage cmdlet 저장 hello 이미지 toohello **시스템** 해당 저장소 계정에서 컨테이너입니다. hello `-DestinationContainername` 매개 변수는 hello 내에서 가상 디렉터리 이름을 **시스템** 컨테이너입니다. hello `-VHDNamePrefix` 매개 변수는 hello blob 이름에 대 한 접두사를 지정 합니다. 이 접두사는 하이픈 앞에 추가 toohello blob 이름입니다. 

    예를 들어 매개 변수 뒤 hello로 저장 AzureRmVMImage를 호출 하는 것으로 가정 합니다.  

        Save-AzureRmVMImage -ResourceGroupName sample-resource-group -Name vm-custom-image -DestinationContainerName batchimages -VHDNamePrefix custom -Path C:\Temp\Images\vm-custom-image.json

    hello 결과 이미지는 여기에 표시 된 blob 이름과 toohello 위치에 저장 됩니다.

    ![system 컨테이너에 저장된 VHD의 위치](media/batch-custom-images/vhd-in-vm-storage-account.png)

    > [!NOTE]
    > Azure 관리되지 않는 VM은 다양한 용도로 여러 저장소 계정을 만듭니다. Hello OS 디스크 때 hello에 대 한 hello 저장소 컨테이너의 hello 이름을 확인 하지 않은 경우 VM이 생성 되었고, 다음 hello hello 연결 된 저장소 계정 찾기에 포함 되어 **시스템** 컨테이너입니다. Hello 탐색 **시스템** 컨테이너 toofind hello 사용자 지정 이미지 hello에 대 한 지정한 값이 hello를 사용 하 여 **저장 AzureRmVMImage** 명령입니다.

## <a name="create-a-pool-from-a-custom-image-in-hello-portal"></a>Hello 포털에서 사용자 지정 이미지에서 풀 만들기

사용자 지정 이미지를 저장했고 해당 위치를 알고 있으면 해당 이미지에서 Batch 풀을 만들 수 있습니다. Hello Azure 포털에서에서 이러한 단계 toocreate 풀을 수행 합니다.

1. Hello Azure 포털에서에서 tooyour 일괄 처리 계정을 이동 합니다. 이 계정은 이어야 하며 동일한 구독 및 지역이 hello 저장소 계정 hello 사용자 지정 이미지를 포함 하 hello에 있습니다. 
2. Hello에 **설정** hello 왼쪽, 선택 hello에서 창을 **풀** 메뉴 항목입니다.
3. Hello에 **풀** 창, 선택 hello **추가** 명령입니다.
4. Hello에 **풀 추가** 창에서 **사용자 지정 이미지 (Linux/Windows)** hello에서 **이미지 유형** 드롭다운입니다. hello를 표시 하는 hello 포털 **사용자 지정 이미지** 선택 합니다. 사용자 지정 이미지 위치한 toohello 저장소 계정을 탐색 하 고 선택 원하는 VHD hello 컨테이너에서 hello 합니다. 
5. 올바른 선택 hello **게시자/제품/Sku** 사용자 지정 VHD에 대 한 합니다.
6. Hello 등의 설정을 필수 hello 남은 지정 **노드 크기**, **대상 전용된 노드에서**, 및 **낮은 우선 순위 노드**뿐만 아니라 원하는 설정 (옵션).

    예를 들어 Microsoft Windows Server Datacenter 2016 사용자 지정 이미지에 대 한 hello **풀 추가** 창이 다음과 같이 나타납니다.

    ![사용자 지정 Windows 이미지에서 풀 추가](media/batch-custom-images/add-pool-custom-image.png)
  
hello을 볼 수는 사용자 지정 이미지를 기반으로 하는 기존 풀 있는지를 toocheck **운영 체제** hello의 hello 리소스 요약 섹션에서 속성 **풀** 창. 너무 설정, 사용자 지정 이미지에서 hello 풀을 만든 경우**사용자 지정 VM 이미지**합니다.

풀에 연결 된 모든 사용자 지정 Vhd hello 풀에 표시 되는 **속성** 창.
 
## <a name="next-steps"></a>다음 단계

- Batch에 대한 심층적인 개요는 [Batch를 사용하여 대규모 병렬 계산 솔루션 개발](batch-api-basics.md)을 참조하세요.
- 일괄 처리 계정 만들기에 대 한 정보를 참조 하십시오. [hello Azure 포털 일괄 처리 계정을 만들고](batch-account-create-portal.md)합니다.
