---
title: "디스크 tooa aaaAttach 클래식 Azure VM | Microsoft Docs"
description: "Hello 클래식 배포 모델을 사용 하 여 만든 데이터 디스크 tooa Windows 가상 컴퓨터를 연결 하 고 초기화 합니다."
services: virtual-machines-windows, storage
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: be4e3e74-05bc-4527-969f-84f10a1d66a7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: cynthn
ms.openlocfilehash: bfe1b0fa066277d28d3862a18da4b1023cb4452d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-virtual-machine-created-with-hello-classic-deployment-model"></a>Hello 클래식 배포 모델을 사용 하 여 만든 데이터 디스크 tooa Windows 가상 컴퓨터를 연결 합니다.
<!--
Refernce article:
    If you want toouse hello new portal, see [How tooattach a data disk tooa Windows VM in hello Azure portal](../../virtual-machines-windows-attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

이 문서에서는 어떻게 tooattach 신규 또는 기존 디스크 hello 클래식 배포 모델 tooa Windows 가상 컴퓨터로 만든 hello를 사용 하 여 Azure 포털을 보여 줍니다.

수도 있습니다 [hello Azure 포털에서에서 데이터 디스크 tooa Linux VM 연결](../../linux/attach-disk-portal.md)합니다.

디스크를 연결하기 전에 다음과 같은 팁을 검토합니다.

* hello 가상 컴퓨터의 hello 크기 첨부할 수 데이터 디스크 수를 제어 합니다. 자세한 내용은 [가상 컴퓨터의 크기](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.

* 프리미엄 저장소 toouse DS 시리즈 또는 GS 시리즈 가상 컴퓨터 필요합니다. 이 가상 컴퓨터를 사용하여 프리미엄 및 표준 저장소 계정에서 모두 디스크를 사용할 수 있습니다. 프리미엄 저장소는 특정 지역에서만 사용할 수 있습니다. 자세한 내용은 [프리미엄 저장소: Azure 가상 컴퓨터 작업을 위한 고성능 저장소](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.

* 새 디스크에 대 한 toocreate 필요 하지 않습니다 것 첫 번째 Azure가 연결 하는 경우 만들기 때문에 있습니다.

또한 [Powershell을 사용하여 데이터 디스크를 연결](../../virtual-machines-windows-attach-disk-ps.md)할 수 있습니다.

> [!IMPORTANT]
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.

## <a name="find-hello-virtual-machine"></a>Hello 가상 컴퓨터를 찾을
1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. 선택 hello hello 대시보드에 나열 된 hello 리소스에서 가상 컴퓨터가 있습니다.
3. Hello 아래 왼쪽된 창에서 **설정**, 클릭 **디스크**합니다.

    ![디스크 설정 열기](./media/attach-disk/virtualmachinedisks.png)

[새 디스크](#option-1-attach-a-new-disk) 또는 [기존 디스크](#option-2-attach-an-existing-disk) 중 하나를 연결하려면 다음 지침에 따라 계속합니다.

## <a name="option-1-attach-and-initialize-a-new-disk"></a>옵션 1: 새 디스크 연결 및 초기화

1. Hello에 **디스크** 블레이드에서 클릭 **새 연결**합니다.
2. Hello 기본 설정을 검토, 필요에 따라 업데이트 한 다음 클릭 **확인**합니다.

   ![디스크 설정 검토](./media/attach-disk/attach-new.png)

3. Azure hello 디스크를 만들고이 toohello 가상 컴퓨터 연결을 새 디스크 hello hello 가상 컴퓨터의 디스크 설정이 아래에 나열 됩니다 **데이터 디스크**합니다.

### <a name="initialize-a-new-data-disk"></a>새 데이터 디스크 초기화

1. Toohello 가상 컴퓨터를 연결 합니다. 자세한 내용은 [어떻게 tooconnect 로그온 tooan Azure 가상 컴퓨터 및 Windows를 실행](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.
2. Toohello 가상 컴퓨터에 로그인 하면 열고 **서버 관리자**합니다. Hello 왼쪽된 창에서 선택 **파일 및 저장소 서비스**합니다.

    ![서버 관리자 열기](../media/attach-disk-portal/fileandstorageservices.png)

3. **디스크**를 선택합니다.
4. hello **디스크** 섹션 hello 디스크를 나열 합니다. 대부분의 경우 가상 컴퓨터에는 디스크 0, 디스크 1, 디스크 2가 있습니다. 디스크 0는 hello 운영 체제 디스크, 디스크 1은 hello 임시 디스크 및 디스크 2는 hello 데이터 디스크가 새로 toohello 가상 컴퓨터를 연결 합니다. hello 데이터 디스크 목록을 hello 파티션으로 **알 수 없는**합니다.

 Hello 디스크를 마우스 오른쪽 단추로 클릭 하 고 선택 **초기화**합니다.

5. Hello 디스크를 초기화 하는 경우 모든 데이터가 삭제 됩니다 알림을 받으면. 클릭 **예** tooacknowledge hello 경고 및 초기화 hello 디스크. 완료 되 면 hello 파티션으로 나열 됩니다 **GPT**합니다. Hello 디스크를 다시 마우스 오른쪽 단추로 클릭 하 고 선택 **새 볼륨**합니다.

6. Hello 기본값을 사용 하는 hello 마법사를 완료 합니다. Hello 마법사가 완료 한 후에 hello **볼륨** 섹션 hello 새 볼륨을 나열 합니다. 이제 hello 디스크가 온라인 상태이 고 준비 toostore 데이터입니다.

    ![볼륨 초기화됨](./media/attach-disk/newdiskafterinitialization.png)

## <a name="option-2-attach-an-existing-disk"></a>옵션 2: 기존 디스크 연결
1. Hello에 **디스크** 블레이드에서 클릭 **연결 기존**합니다.
2. **기존 디스크 연결**에서 **위치**를 클릭합니다.

   ![기존 디스크 연결](./media/attach-disk/attachexistingdisksettings.png)
3. 아래 **저장소 계정은**, hello 계정과 hello.vhd 파일을 보유 하는 컨테이너를 선택 합니다.

   ![VHD 위치 찾기](./media/attach-disk/existdiskstorageaccountandcontainer.png)

4. Hello.vhd 파일을 선택 합니다.
5. 아래 **기존 디스크 연결**, 방금 선택한 hello 파일 아래에 있는지 **VHD 파일**합니다. **확인**을 클릭합니다.
6. Azure 연결 hello 디스크 toohello 가상 컴퓨터, hello 가상 컴퓨터의 디스크 설정이 아래에 나열 됩니다 **데이터 디스크**합니다.

## <a name="use-trim-with-standard-storage"></a>표준 저장소와 TRIM 사용

표준 저장소(HDD)를 사용하는 경우 TRIM을 사용하도록 설정해야 합니다. TRIM 실제로 사용 하는 저장소에 대 한만 청구 됩니다 하므로 hello 디스크에 사용 하지 않는 블록을 삭제 합니다. TRIM을 사용하면 큰 파일의 삭제로 발생하는 사용되지 않는 블록을 포함하여 비용을 절약할 수 있습니다.

이 명령은 toocheck hello 트림 설정을 실행할 수 있습니다. Windows VM에서 명령 프롬프트를 열어 다음을 입력합니다.

```
fsutil behavior query DisableDeleteNotify
```

Hello 명령이 0을 반환 하는 경우 TRIM 올바르게 활성화 됩니다. 1을 반환 하는 경우 다음 명령을 tooenable TRIM hello를 실행 합니다.
```
fsutil behavior set DisableDeleteNotify 0
```

## <a name="next-steps"></a>다음 단계
응용 프로그램 toouse hello d: 드라이브 toostore 데이터를 필요한 경우 다음을 할 수 있습니다 [hello Windows 임시 디스크의 드라이브 문자 hello 변경](../../virtual-machines-windows-change-drive-letter.md)합니다.

## <a name="additional-resources"></a>추가 리소스
[가상 컴퓨터용 디스크 및 VHD에 대하여](../../virtual-machines-linux-about-disks-vhds.md)
