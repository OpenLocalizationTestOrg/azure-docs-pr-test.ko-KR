---
title: "Azure 저장소 계정, 컨테이너 또는 Vhd를 삭제 하면 aaaTroubleshoot 오류 | Microsoft Docs"
description: "Azure Storage 계정, 컨테이너 또는 VHD를 삭제하는 경우 발생하는 오류 문제 해결"
services: storage
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: storage
ms.assetid: 17403aa1-fe8d-45ec-bc33-2c0b61126286
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 77361593e2c924d39aba853e0807dc3188f50e60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-errors-when-you-delete-azure-storage-accounts-containers-or-vhds"></a>Azure Storage 계정, 컨테이너 또는 VHD를 삭제하는 경우 발생하는 오류 문제 해결

오류가 발생할 수 있습니다는 Azure 저장소 계정, 컨테이너 또는 가상 하드 디스크 (VHD) toodelete 할 때 hello에 [Azure 포털](https://portal.azure.com)합니다. 이 문서에서는 Azure 리소스 관리자 배포에서 가이드 toohelp 해결 hello 문제를 해결 합니다.

이 문서는 Azure 문제 해결 되지 않습니다를 방문 하 여 Azure 포럼에 hello [MSDN 및 스택 오버플로](https://azure.microsoft.com/support/forums/)합니다. 이러한 포럼에 문제를 게시할 수 있습니다 또는 too@AzureSupport Twitter에서. 또한 선택 하 여 Azure 지원 요청을 제출할 수 있습니다 **지원을 받는** hello에 [Azure 지원](https://azure.microsoft.com/support/options/) 사이트입니다.

## <a name="symptoms"></a>증상
### <a name="scenario-1"></a>시나리오 1
리소스 관리자 배포에서 저장소 계정에 VHD toodelete을 시도할 때 hello 다음과 같은 오류 메시지가 나타납니다.

**Toodelete blob 'vhds/BlobName.vhd'에 실패 했습니다. 오류: 현재 임대에 hello blob 있고 hello 요청에 임대 ID가 없습니다. 지정 되었습니다.**

가상 컴퓨터 (VM) hello toodelete를 시도 하는 VHD 한 임 대권을 있으므로이 문제가 발생할 수 있습니다.

### <a name="scenario-2"></a>시나리오 2
리소스 관리자 배포에서 저장소 계정에서 컨테이너 toodelete을 시도할 때 hello 다음과 같은 오류 메시지가 나타납니다.

**Vhd를' toodelete 저장소 컨테이너'에 실패 했습니다. 오류: 현재 임대에 hello 컨테이너 있고 hello 요청에 임대 ID가 없습니다. 지정 되었습니다.**

이 문제는 hello 컨테이너 임대 상태 hello에에서 잠겨 있는 VHD에 있기 때문에 발생할 수 있습니다.

### <a name="scenario-3"></a>시나리오 3
리소스 관리자 배포에서 저장소 계정을 toodelete을 시도할 때 hello 다음과 같은 오류 메시지가 나타납니다.

**Toodelete 저장소 계정 'StorageAccountName'에 실패 했습니다. 오류: tooits 아티팩트가 사용 중이기 때문 hello 저장소 계정을 삭제할 수 없습니다.**

이 문제는 hello 저장소 계정 hello 임대 상태에 있는 VHD를 포함 하기 때문에 발생할 수 있습니다.

## <a name="solution"></a>해결 방법 
tooresolve hello VM에 연결 하 고 이러한 문제를 hello hello 오류가 발생 하는 VHD를 식별 해야 합니다. 그런 다음 (데이터 디스크)에 대 한 hello VM에서에서 VHD hello를 분리 하거나 hello hello VHD (OS 디스크)를 사용 하는 VM을 삭제 합니다. 이 hello 임대 hello VHD에서에서 제거 하 고 삭제 toobe 허용 합니다. 

toodo,이 중 하나를이 사용 메서드를 다음 hello:

### <a name="method-1---use-azure-storage-explorer"></a>방법 1 - Azure Storage 탐색기 사용

### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a>1 단계 확인 hello hello 저장소 계정 삭제를 방지 하는 VHD

1. Hello 저장소 계정을 삭제 하면 hello 다음과 같은 메시지 대화 상자가 표시 됩니다. 

    ![hello 저장소 계정을 삭제할 때 메시지](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. Hello 확인 **디스크 URL** tooidentify hello 저장소 계정 및 hello 하지 못한다는 VHD hello 저장소 계정을 삭제 합니다. Hello 하기 전에 두 문자열의 다음 예제는 hello, ". blob.core.windows.net" hello 저장소 계정 이름이 며, "SCCM2012-2015-08-28.vhd" hello VHD 이름입니다.  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

### <a name="step-2-delete-hello-vhd-by-using-azure-storage-explorer"></a>Azure 저장소 탐색기를 사용 하 여 2 단계 삭제 hello VHD

1. 다운로드 및 설치 최신 버전의 hello [Azure 저장소 탐색기](http://storageexplorer.com/)합니다. 이 도구는 microsoft Windows, macOS 및 Linux에서 데이터를 Azure 저장소 사용 tooeasily 작업을 허용 하는 독립 실행형 앱입니다.
2. Azure Storage 탐색기를 열고 왼쪽 막대에서 ![계정 아이콘](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/account.png) hello 왼쪽된 모음에서 Azure 환경을 선택한 다음에 로그인 합니다.

3. 모든 구독 또는 toodelete 원하는 hello 저장소 계정이 포함 된 hello 구독을 선택 합니다.

    ![구독 추가](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/addsub.png)

4. Hello 디스크 URL 앞에서 hello에서를 얻 었 toohello 저장소 계정을 이동 **Blob 컨테이너** > **vhd** hello 저장소 계정을 삭제 하지 못한다는 VHD hello에 대 한 검색 합니다.
5. Hello VHD 발견 되 면 hello 확인 **VM 이름** toofind hello VM이이 VHD를 사용 하는 열입니다.

    ![VM 확인](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/check-vm.png)

6. Azure 포털을 사용 하 여 hello VHD에서에서 hello 임대를 제거 합니다. 자세한 내용은 참조 [hello VHD에서에서 제거 hello 임대](#remove-the-lease-from-the-vhd)합니다. 

7. Toohello Azure 저장소 탐색기로 이동 하 고 hello VHD를 마우스 오른쪽 단추로 클릭 한 다음 삭제를 선택 합니다.

8. Hello 저장소 계정을 삭제 합니다.

### <a name="method-2---use-azure-portal"></a>방법 2 - Azure Portal 사용 

#### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a>1 단계: hello hello 저장소 계정 삭제를 방지 하는 VHD를 식별 합니다.

1. Hello 저장소 계정을 삭제 하면 hello 다음과 같은 메시지 대화 상자가 표시 됩니다. 

    ![hello 저장소 계정을 삭제할 때 메시지](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. Hello 확인 **디스크 URL** tooidentify hello 저장소 계정 및 hello 하지 못한다는 VHD hello 저장소 계정을 삭제 합니다. Hello 하기 전에 두 문자열의 다음 예제는 hello, ". blob.core.windows.net" hello 저장소 계정 이름이 며, "SCCM2012-2015-08-28.vhd" hello VHD 이름입니다.  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

2. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
3. Hello 허브 메뉴에서 선택 **모든 리소스**합니다. Toohello 저장소 계정을 선택한 후 선택 **Blob** > **vhd**합니다.

    ![Hello 저장소 계정 및 강조 표시 하는 hello "vhd" 컨테이너와 hello 포털의 스크린샷](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/opencontainer.png)

4. Hello를 이전 hello 디스크 URL에서 가져온 VHD를 찾습니다. 그런 다음 VM을 사용 하 여 결정 VHD hello 합니다. 일반적으로, VM hello VHD의 이름을 확인 하 여 hello VHD를 보유 하는 확인할 수 있습니다.

Resource Manager 개발 모델의 VM

   * OS 디스크는 일반적으로 VMName-YYYY-MM-DD-HHMMSS.vhd 명명 규칙을 따릅니다.
   * 데이터 디스크는 일반적으로 VMName-YYYY-MM-DD-HHMMSS.vhd 명명 규칙을 따릅니다.

Classic 개발 모델의 VM

   * OS 디스크는 일반적으로 CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd 명명 규칙을 따릅니다.
   * 데이터 디스크는 일반적으로 CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd 명명 규칙을 따릅니다.

#### <a name="step-2-remove-hello-lease-from-hello-vhd"></a>2 단계: hello VHD에서에서 hello 임대를 제거 합니다.

[Hello 임대 hello VHD에서에서 제거](#remove-the-lease-from-the-vhd), 한 다음 hello 저장소 계정을 삭제 합니다.

## <a name="what-is-a-lease"></a>임대란?
임대는 사용 되는 toocontrol 액세스 tooa blob (VHD 등) 일 수 있는 잠금입니다. Blob를 임대할 hello blob hello 임대의 hello 소유자만 액세스할 수 있습니다. 임대가 이유 뒤 hello에 대 한 중요 합니다.

* 여러 소유자 toowrite toohello 시도 하는 경우 데이터가 손상 되지 않게 hello에 hello blob의 동일한 부분이 동시 합니다.
* Hello blob 항목 적극적으로 사용 하는 경우 (예를 들어 VM)이 삭제 되지 않도록 방지 합니다.
* Hello 저장소 계정 항목 적극적으로 사용 하는 경우 (예를 들어 VM)이 삭제 되지 않도록 방지 합니다.

### <a name="remove-hello-lease-from-hello-vhd"></a>Hello VHD에서에서 hello 임대를 제거 합니다.
Hello VHD는 운영 체제 디스크를 hello VM tooremove hello 임대를 삭제 해야 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello에 **허브** 메뉴 선택 **가상 컴퓨터**합니다.
3. Hello hello VHD에 임대를 보유 하는 VM을 선택 합니다.
4. 아무 것도 적극적으로 사용 hello 가상 컴퓨터와는 하면 더 이상 필요 hello 가상 컴퓨터를 확인 합니다.
5. Hello의 hello 위쪽 **VM 세부 정보** 블레이드를 **삭제**, 클릭 하 고 **예** tooconfirm 합니다.
6. hello VM은 삭제 되어야 하지만 hello VHD를 보존할 수 있습니다. 그러나 hello VHD 해야에 더 이상 없는 임대 것입니다. Hello 임대 toobe 출시 몇 분 정도 걸릴 수 있습니다. 임대 hello tooverify 릴리스, 너무 이동**모든 리소스** > **저장소 계정 이름** > **Blob**  >  **vhd**합니다. Hello에 **속성 Blob** 창, hello **임대 상태** 값 해야 **잠금 해제 됨**합니다.

데이터 디스크 VHD hello 이면 hello VM tooremove hello 임대에서 hello VHD를 분리 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello에 **허브** 메뉴 선택 **가상 컴퓨터**합니다.
3. Hello hello VHD에 임대를 보유 하는 VM을 선택 합니다.
4. 선택 **디스크** hello에 **VM 세부 정보** 블레이드입니다.
5. Hello VHD에 임대를 보유 하는 hello 데이터 디스크를 선택 합니다. VHD에 연결 된 확인할 수 있습니다 hello VHD의 hello URL을 확인 하 여 hello 디스크.
6. 아무 것도 적극적으로 사용 하 고 있는지 hello 데이터 디스크 확실 하 게 결정 합니다.
7. 클릭 **분리** hello에 **세부 정보를 디스크** 블레이드입니다.
8. hello 디스크 VM hello에서 분리할 수 이제 해야 하며, VHD hello 더 이상 임대에 없습니다. Hello 임대 toobe 출시 몇 분 정도 걸릴 수 있습니다. 해제 된 임대 hello tooverify, 너무 이동**모든 리소스** > **저장소 계정 이름** > **Blob**  >  **vhd**합니다. Hello에 **속성 Blob** 창, hello **임대 상태** 값 해야 **잠금 해제 됨**합니다.

## <a name="next-steps"></a>다음 단계
* [저장소 계정 삭제](storage-create-storage-account.md#delete-a-storage-account)
* [Toobreak hello (PowerShell) Microsoft Azure에서 blob 저장소의 임대를 잠그는 방법을](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)
