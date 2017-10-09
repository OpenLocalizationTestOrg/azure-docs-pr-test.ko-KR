---
title: "데이터 디스크 tooa Linux VM aaaAttach | Microsoft Docs"
description: "어떻게 tooattach 새로운 또는 기존의 데이터 디스크 tooa Linux VM에 Azure 포털 사용 하 여 hello hello 리소스 관리자 배포 모델입니다."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5e1c6212-976c-4962-a297-177942f90907
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: cynthn
ms.openlocfilehash: 069c3c6f5e71a8c495342e6d0c6f3d92c4ed5053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-vm-in-hello-azure-portal"></a>Tooattach 데이터 hello Azure 포털에서에서 Linux VM tooa 디스크 하는 방법
이 문서에서는 신규 및 기존 tooattach hello Azure 포털을 통해 tooa Linux 가상 컴퓨터 디스크 하는 방법을 설명 합니다. 수도 있습니다 [hello Azure 포털에서에서 데이터 디스크 tooa Windows VM 연결](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. Toouse Azure 관리 되는 디스크 중 하나를 선택할 수 있습니다 또는 디스크 관리 되지 않는 합니다. 관리 되는 디스크 hello Azure 플랫폼에서 처리 되 고 모든 준비 단계 또는 위치 toostore 필요 하지 않은 하 합니다. 관리되지 않는 디스크는 저장소 계정이 필요하며 [적용되는 할당량 및 제한](../../azure-subscription-service-limits.md#storage-limits)이 있습니다. Azure Managed Disks에 대한 자세한 내용은 [Azure Managed Disks 개요](../windows/managed-disks-overview.md)를 참조하세요.

디스크 tooyour VM을 연결 하기 전에 다음이 팁을 검토 합니다.

* hello 가상 컴퓨터의 hello 크기 첨부할 수 데이터 디스크 수를 제어 합니다. 자세한 내용은 [가상 컴퓨터의 크기](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.
* 프리미엄 저장소 toouse DS 시리즈 또는 GS 시리즈 가상 컴퓨터 필요합니다. 이러한 가상 컴퓨터와 함께 프리미엄 및 표준 디스크를 모두 사용할 수 있습니다. 프리미엄 저장소는 특정 지역에서만 사용할 수 있습니다. 자세한 내용은 [프리미엄 저장소: Azure 가상 컴퓨터 작업을 위한 고성능 저장소](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.
* 디스크 연결 된 toovirtual 컴퓨터는 Azure에 저장 된.vhd 파일 실제로입니다. 자세한 내용은 [가상 컴퓨터용 디스크 및 VHD 정보](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.


## <a name="find-hello-virtual-machine"></a>Hello 가상 컴퓨터를 찾을
1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. Hello 허브 메뉴에서 클릭 **가상 컴퓨터**합니다.
3. Hello 목록에서 hello 가상 컴퓨터를 선택 합니다.
4. toohello 가상 컴퓨터에서 블레이드에서 **Essentials**, 클릭 **디스크**합니다.
   
    ![디스크 설정 열기](./media/attach-disk-portal/find-disk-settings.png)

[관리되는 디스크](#use-azure-managed-disks) 또는 [관리되지 않는 디스크](#use-unmanaged-disks) 중 하나를 연결하려면 다음 지침에 따라 계속합니다.

## <a name="use-azure-managed-disks"></a>Azure Managed Disks 사용

### <a name="attach-a-new-disk"></a>새 디스크 연결

1. Hello에 **디스크** 블레이드에서 클릭 **+ 추가 데이터 디스크**합니다.
2. Hello 드롭다운 메뉴를 클릭 **이름** 선택 **만들기 디스크**:

    ![Azure Managed Disks 만들기](./media/attach-disk-portal/create-new-md.png)

3. 관리되는 디스크에 대한 이름을 입력합니다. Hello 기본 설정을 검토, 필요에 따라 업데이트 한 다음 클릭 **만들기**합니다.
   
   ![디스크 설정 검토](./media/attach-disk-portal/create-new-md-settings.png)

4. 클릭 **저장** toocreate hello 디스크 및 업데이트 hello VM 구성을 관리 합니다.

   ![새 Azure Managed Disk 저장](./media/attach-disk-portal/confirm-create-new-md.png)

5. Azure hello 디스크를 만들고이 toohello 가상 컴퓨터 연결을 새 디스크 hello hello 가상 컴퓨터의 디스크 설정이 아래에 나열 됩니다 **데이터 디스크**합니다. 관리 되는 디스크는 최상위 리소스를 hello 디스크 hello 리소스 그룹의 hello 루트에 나타납니다.

   ![리소스 그룹의 Azure Managed Disk](./media/attach-disk-portal/view-md-resource-group.png)

### <a name="attach-an-existing-disk"></a>기존 디스크 연결
1. Hello에 **디스크** 블레이드에서 클릭 **+ 추가 데이터 디스크**합니다.
2. Hello 드롭다운 메뉴를 클릭 **이름** tooview 기존 목록은 디스크 액세스할 수 있는 tooyour Azure 구독을 관리 합니다. 관리 되는 select hello 디스크 tooattach:

   ![기존 Azure Managed Disk 연결](./media/attach-disk-portal/select-existing-md.png)

3. 클릭 **저장** tooattach hello 기존 관리 하는 디스크와 업데이트 hello VM 구성:
   
   ![Azure Managed Disk 업데이트 저장](./media/attach-disk-portal/confirm-attach-existing-md.png)

4. Azure 연결 hello 디스크 toohello 가상 컴퓨터, hello 가상 컴퓨터의 디스크 설정이 아래에 나열 됩니다 **데이터 디스크**합니다.

## <a name="use-unmanaged-disks"></a>관리되지 않는 디스크 사용

### <a name="attach-a-new-disk"></a>새 디스크 연결

1. Hello에 **디스크** 블레이드에서 클릭 **+ 추가 데이터 디스크**합니다.
2. Hello 기본 설정을 검토, 필요에 따라 업데이트 한 다음 클릭 **확인**합니다.
   
   ![디스크 설정 검토](./media/attach-disk-portal/attach-new.png)
3. Azure hello 디스크를 만들고이 toohello 가상 컴퓨터 연결을 새 디스크 hello hello 가상 컴퓨터의 디스크 설정이 아래에 나열 됩니다 **데이터 디스크**합니다.

### <a name="attach-an-existing-disk"></a>기존 디스크 연결
1. Hello에 **디스크** 블레이드에서 클릭 **+ 추가 데이터 디스크**합니다.
2. **기존 디스크 연결**에서 **VHD 파일**을 클릭합니다.
   
   ![기존 디스크 연결](./media/attach-disk-portal/attach-existing.png)
3. 아래 **저장소 계정은**, hello 계정과 hello.vhd 파일을 보유 하는 컨테이너를 선택 합니다.
   
   ![VHD 위치 찾기](./media/attach-disk-portal/find-storage-container.png)
4. Hello.vhd 파일을 선택 합니다.
5. 아래 **기존 디스크 연결**, 방금 선택한 hello 파일 아래에 있는지 **VHD 파일**합니다. **확인**을 클릭합니다.
6. Azure 연결 hello 디스크 toohello 가상 컴퓨터, hello 가상 컴퓨터의 디스크 설정이 아래에 나열 됩니다 **데이터 디스크**합니다.


## <a name="next-steps"></a>다음 단계
Tooprepare hello 디스크를 추가한 후 필요한 사용 하기 위해. 자세한 내용은 [방법: Linux에서 새 데이터 디스크 초기화](add-disk.md)를 참조하세요.
