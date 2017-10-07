---
title: "클래식 배포에서 Azure 저장소 계정, 컨테이너 또는 Vhd를 삭제 하는 aaaTroubleshoot | Microsoft Docs"
description: "클래식 배포에서 Azure 저장소 계정, 컨테이너 또는 VHD를 삭제하는 문제 해결"
services: storage
documentationcenter: 
author: genlin
manager: felixwu
editor: tysonn
tags: storage
ms.assetid: 0f7a8243-d8dc-432a-9d37-1272a0cb3a5c
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 6bbfa032e1968718c623227bb426d553e2951075
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deleting-azure-storage-accounts-containers-or-vhds-in-a-classic-deployment"></a>클래식 배포에서 Azure 저장소 계정, 컨테이너 또는 VHD를 삭제하는 문제 해결
[!INCLUDE [storage-selector-cannot-delete-storage-account-container-vhd](../../includes/storage-selector-cannot-delete-storage-account-container-vhd.md)]

Hello에 toodelete hello Azure 저장소 계정, 컨테이너 또는 VHD를 시도 하는 경우 오류가 발생할 수 있습니다 [Azure 포털](https://portal.azure.com/) 또는 hello [Azure 클래식 포털](https://manage.windowsazure.com/)합니다. hello 문제 hello 다음 상황에서 발생할 수 있습니다.

* VM을 삭제 하면 hello 디스크 및 VHD 하지 자동으로 삭제 됩니다. 저장소 계정 삭제에 실패에 대 한 hello 이유는 수도 있습니다. 다른 VM 디스크 toomount hello를 사용할 수 있도록 hello 디스크를 삭제 하지 마십시오 했습니다.
* Hello 디스크와 연결 된 디스크 또는 hello blob에서 임대는 여전히 합니다.
* Blob, 컨테이너 또는 저장소 계정을 사용하는 VM 이미지는 여전히 있습니다.

이 문서의 Azure 문제 해결 되지 않으면 방문 하 여 Azure 포럼에 hello [MSDN 스택 오버플로 hello 및](https://azure.microsoft.com/support/forums/)합니다. 이러한 포럼에 문제를 게시할 수 있습니다 또는 too@AzureSupport Twitter에서. 또한 선택 하 여 Azure 지원 요청을 제출할 수 있습니다 **지원을 받는** hello에 [Azure 지원](https://azure.microsoft.com/support/options/) 사이트입니다.

## <a name="symptoms"></a>증상
다음 섹션 hello toodelete hello Azure 저장소 계정, 컨테이너 또는 Vhd를 시도 하는 경우 나타날 수 있는 일반적인 오류를 나열 합니다.

### <a name="scenario-1-unable-toodelete-a-storage-account"></a>시나리오 1: 수 없습니다 toodelete 저장소 계정
Hello에서 toohello 클래식 저장소 계정을 탐색 하는 경우 [Azure 포털](https://portal.azure.com/) 선택 **삭제**, hello 저장소 계정 삭제를 방지 하는 개체의 목록으로 제공 될 수 있습니다.

  ![오류의 이미지 hello 저장소 계정 삭제](./media/storage-cannot-delete-storage-account-container-vhd/newerror.png)

Hello toohello 저장소 계정의 탐색 하는 경우 [Azure 클래식 포털](https://manage.windowsazure.com/) 선택 **삭제**, hello 다음 오류 중 하나가 나타날 수 있습니다.

- *저장소 계정 StorageAccountName에는 VM 이미지가 들어 있습니다. 이 저장소 계정을 삭제하려면 이러한 VM 이미지를 제거해야 합니다.*

- *저장소 계정 toodelete < vm-저장소 계정-이름 >에 실패 했습니다. 저장소 계정 수 없습니다 toodelete < vm-저장소 계정-이름 >: ' 저장소 계정 < vm-저장소 계정-이름 >에 일부 활성 이미지 및/또는 디스크. 이 저장소 계정을 삭제하려면 이러한 이미지 및/또는 디스크를 제거해야 합니다.'.*

- *저장소 계정 <vm-storage-account-name>에 xxxxxxxxx- xxxxxxxxx-O-209490240936090599과(와) 같은 일부 활성 이미지 및/또는 디스크가 있습니다. 이 저장소 계정을 삭제하려면 이러한 이미지 및/또는 디스크를 제거해야 합니다.*

- *저장소 계정 <vm-storage-account-name>에 활성 이미지 및/또는 디스크 아티팩트를 포함하는 1 컨테이너가 있습니다. 이 저장소 계정을 삭제 하기 전에 이러한 아티팩트가 hello 이미지 리포지토리에서 제거 되었는지 확인*합니다.

- *제출 실패 저장소 계정 <vm-storage-account-name>에 활성 이미지 및/또는 디스크 아티팩트를 포함하는 1 컨테이너가 있습니다. 이러한 아티팩트가이 저장소 계정을 삭제 하기 전에 hello 이미지 리포지토리에서 제거 되었는지 확인 합니다. Toobe 삭제 해야 하는 활성 디스크가 있는지를 알려 주는 메시지가 표시는 toodelete 저장소 계정을 사용 하려는 경우 여전히 활성 디스크가 연결 되어 있는지*합니다.

### <a name="scenario-2-unable-toodelete-a-container"></a>시나리오 2: 수 없습니다 toodelete 컨테이너
Toodelete hello 저장소 컨테이너를 보려는 경우 hello 다음 오류가 표시 될 수 있습니다.

*실패 한 toodelete 저장소 컨테이너 <container name>합니다. 오류: ' hello 컨테이너에서 임대 현재는 고 hello 요청에 임대 ID가 없습니다. 지정 된*합니다.

또는

*가상 컴퓨터 디스크를 수행 하는 hello 사용 하 여이 컨테이너의 blob hello 컨테이너를 삭제할 수 없습니다: VirtualMachineDiskName1, VirtualMachineDiskName2,...*

### <a name="scenario-3-unable-toodelete-a-vhd"></a>시나리오 3: 수 없습니다 toodelete VHD
VM을 삭제 한 후 시도 toodelete hello blob hello에 대 한 Vhd를 연결 하는 다음 hello 메시지의 뒤에 나타날 수 있습니다.

*실패 한 toodelete blob ' 경로/XXXXXX-XXXXXX-os-1447379084699.vhd'. 오류: ' hello blob에서 임대 현재는 고 hello 요청에 임대 ID가 없습니다. 지정 된 합니다.*

또는

*Blob 'BlobName.vhd' 가상 컴퓨터 디스크 'VirtualMachineDiskName' 사용 중에서 이므로 hello blob을 삭제할 수 없습니다.*

## <a name="solution"></a>해결 방법
tooresolve hello 가장 일반적인 문제 메서드 뒤 hello를 시도해 보십시오.

### <a name="step-1-delete-any-disks-that-are-preventing-deletion-of-hello-storage-account-container-or-vhd"></a>1 단계: hello 저장소 계정, 컨테이너 또는 VHD의 삭제를 방지 하는 모든 디스크를 삭제 합니다.
1. Toohello 전환 [Azure 클래식 포털](https://manage.windowsazure.com/)합니다.
2. **가상 컴퓨터** > **디스크**를 선택합니다.

    ![Azure 클래식 포털에 표시된 가상 컴퓨터의 디스크 이미지입니다.](./media/storage-cannot-delete-storage-account-container-vhd/VMUI.png)
3. Hello 저장소 계정, 컨테이너 또는 toodelete 원하는 VHD와 연결 된 hello 디스크를 찾습니다. Hello 디스크의 hello 위치를 확인 하는 경우 저장소 계정, 컨테이너 또는 VHD hello 연결을 찾을 수 있습니다.

    ![Azure 클래식 포털에서 디스크의 위치 정보를 보여주는 이미지](./media/storage-cannot-delete-storage-account-container-vhd/DiskLocation.png)
4. Hello 메서드를 다음 중 하나를 사용 하 여 hello 디스크를 삭제 합니다.

  - Hello에 없는 VM 나열 없을 경우 **에 연결 된** 필드 hello 디스크의 hello 디스크를 직접 삭제할 수 있습니다.

  - Hello 디스크 데이터 디스크가 다음이 단계를 따르십시오.

    1. 디스크 hello VM에 연결 된 hello hello 이름을 확인 하십시오.
    2. 너무 이동**가상 컴퓨터** > **인스턴스**, 한 다음 VM hello를 찾습니다.
    3. 아무 것도 적극적으로 사용 하 고 있는지 hello 디스크 있는지 확인 합니다.
    4. 선택 **디스크 분리** hello 포털 toodetach hello 디스크 hello 맨 아래에 있습니다.
    5. 너무 이동**가상 컴퓨터** > **디스크**, hello 기다립니다 **에 연결 된** 빈 필드 tooturn 합니다. 이 hello 디스크 hello VM에서에서 성공적으로 분리 된 것을 나타냅니다.
    6. 선택 **삭제** hello 맨 아래에 **가상 컴퓨터** > **디스크** toodelete hello 디스크.

  - Hello 디스크는 운영 체제 디스크는 경우 (hello **OS 포함** Windows와 같은 필드에 값) 및 다음이 단계를 수행 하는 연결 된 tooa VM을 toodelete hello VM입니다. toodelete hello VM toorelease hello 임대 해야 hello OS 디스크를 분리할 수 없습니다.

    1. 데이터 디스크에 연결 되어 hello 가상 컴퓨터 hello hello 이름을 확인 하십시오.  
    2. 너무 이동**가상 컴퓨터** > **인스턴스**을 다음 선택 hello hello 디스크를 VM에 첨부 하 고 있습니다.
    3. 아무 것도 적극적으로 사용 hello 가상 컴퓨터와는 하면 더 이상 필요 hello 가상 컴퓨터를 확인 합니다.
    4. 선택 hello VM hello 디스크에 연결 되어, 다음 선택 **삭제** > **연결 된 디스크 삭제 hello**합니다.
    5. 너무 이동**가상 컴퓨터** > **디스크**, hello 디스크 toodisappear 될 때까지 기다립니다.  이 toooccur 몇 분 정도 걸릴 수 있습니다 및 toorefresh hello 페이지를 할 수 있습니다.
    6. Hello 디스크 사라지지 않는 경우 hello에 대 한 대기 **에 연결 된** 빈 필드 tooturn 합니다. 이 hello 디스크 hello VM에서에서 완벽 하 게 분리 된 것을 나타냅니다.  그런 다음 hello 디스크를 선택 하 고 선택 **삭제** hello 페이지 toodelete hello 디스크 hello 맨 아래에 있습니다.


   > [!NOTE]
   > 연결 된 tooa VM 디스크가 있는 경우 됩니다 수 toodelete 것입니다. 디스크는 삭제된 VM에서 비동기적으로 분리됩니다. 이 필드 tooclear에 대 한 hello VM은 삭제 후 몇 분이 걸릴 수 있습니다.
   >
   >


### <a name="step-2-delete-any-vm-images-that-are-preventing-deletion-of-hello-storage-account-or-container"></a>2 단계: hello 저장소 계정 또는 컨테이너의 삭제를 방지 하는 모든 VM 이미지를 삭제 합니다.
1. Toohello 전환 [Azure 클래식 포털](https://manage.windowsazure.com/)합니다.
2. 선택 **가상 컴퓨터** > **이미지**, hello 저장소 계정, 컨테이너 또는 VHD와 연결 된 hello 이미지를 삭제 합니다.

    그 후 다시 toodelete hello 저장소 계정, 컨테이너 또는 VHD 시도 합니다.

> [!WARNING]
> Hello 계정을 삭제 하기 전에 toosave를 원하는 있는지 tooback 향상 됩니다. VHD, BLOB, 테이블, 큐 또는 파일을 삭제하면 영구적으로 삭제됩니다. Hello 리소스 사용 중임을 확인 합니다.
>
>

## <a name="about-hello-stopped-deallocated-status"></a>Hello 중지 됨 (할당 취소 됨) 상태에 대 한
유지 된 경우가 hello 클래식 배포 모델에서 만들어진 Vm hello 갖습니다 **중지 됨 (할당 취소 됨)** 상태 중 하나가 hello에 [Azure 포털](https://portal.azure.com/) 또는 [Azure 클래식 포털 ](https://manage.windowsazure.com/).

**Azure 클래식 포털**:

![Azure 포털에 표시된 VM의 중지됨(할당 취소됨) 상태입니다.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo2.png)

**Azure 포털**:

![Azure 클래식 포털에 표시된 VM의 중지됨(할당 취소됨) 상태입니다.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo1.png)

"중지 됨 (할당 취소 됨)" 상태 hello CPU, 메모리 및 네트워크와 같은 hello 컴퓨터 리소스를 해제합니다. 그러나 hello 디스크를 신속 하 게 다시 만들 수 있습니다 hello VM 필요한 경우 아직 보존 되어 있습니다. 이러한 디스크는 Azure 저장소에서 지원하는 VHD를 기반으로 만들어집니다. hello 저장소 계정에 이러한 Vhd 및 hello 디스크는 Vhd에 임대가 있습니다.

## <a name="next-steps"></a>다음 단계
* [저장소 계정 삭제](storage-create-storage-account.md#delete-a-storage-account)
