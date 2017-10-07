---
title: "관리 되지 않는 데이터 디스크 tooa Windows VM-Azure aaaAttach | Microsoft Docs"
description: "어떻게 tooattach 새로운 또는 기존의 관리 되지 않는 데이터 디스크 tooa Windows VM에 Azure 포털 사용 하 여 hello hello 리소스 관리자 배포 모델입니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3790fc59-7264-41df-b7a3-8d1226799885
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: 923a6663974143bf359970f9b0eb0d36cabcba9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-an-unmanaged-data-disk-tooa-windows-vm-in-hello-azure-portal"></a>Tooattach 관리 되지 않는 데이터 hello Azure 포털에서에서 tooa Windows VM 디스크 하는 방법

이 문서에서는 hello Azure 포털을 통해 tooWindows 가상 컴퓨터 디스크 tooattach 신규 및 기존 관리 되지 않는 합니다. 또한 [PowerShell을 사용하여 데이터 디스크를 연결](./attach-disk-ps.md)할 수 있습니다. 이 작업을 수행 하기 전에 다음 팁을 검토하세요.

* hello 가상 컴퓨터의 hello 크기 첨부할 수 데이터 디스크 수를 제어 합니다. 자세한 내용은 [가상 컴퓨터의 크기](sizes.md)를 참조하세요.
* 프리미엄 저장소 toouse DS 시리즈 또는 GS 시리즈 가상 컴퓨터 필요합니다. 이 가상 컴퓨터를 사용하여 프리미엄 및 표준 저장소 계정에서 모두 디스크를 사용할 수 있습니다. 프리미엄 저장소는 특정 지역에서만 사용할 수 있습니다. 자세한 내용은 [프리미엄 저장소: Azure 가상 컴퓨터 작업을 위한 고성능 저장소](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.
* 새 디스크에 대 한 toocreate 필요 하지 않습니다 것 첫 번째 Azure가 연결 하는 경우 만들기 때문에 있습니다.


또한 [Powershell을 사용하여 데이터 디스크를 연결](attach-disk-ps.md)할 수 있습니다.


## <a name="find-hello-virtual-machine"></a>Hello 가상 컴퓨터를 찾을
1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. Hello hello 왼쪽 메뉴를 클릭 **가상 컴퓨터**합니다.
3. Hello 목록에서 hello 가상 컴퓨터를 선택 합니다.
4. Hello 가상 컴퓨터 블레이드 클릭 **디스크**합니다.
   
[새 디스크](#option-1-attach-a-new-disk) 또는 [기존 디스크](#option-2-attach-an-existing-disk) 중 하나를 연결하려면 다음 지침에 따라 계속합니다.

## <a name="option-1-attach-and-initialize-a-new-disk"></a>옵션 1: 새 디스크 연결 및 초기화
1. Hello에 **디스크** 블레이드에서 클릭 **+ 추가 데이터 디스크**합니다.
2. Hello에 **연결 관리 되는 디스크** 블레이드에서 hello 디스크의 이름 입력 **이름** 선택한 후 **새로 만들기 (빈 디스크)** 에 **소스 형식**합니다.
3. 아래 **저장소 컨테이너**, hello 클릭 **찾아보기** 단추 및 toohello 저장소 계정 및 컨테이너를 hello 새 VHD toobe 저장 선택한 다음 클릭 찾아보기 **선택**. 
  
   ![디스크 설정 검토](./media/attach-disk-portal/attach-empty-unmanaged.png)
   
3. Hello 데이터 디스크에 대 한 hello 설정을 사용 하 여 작업을 완료 클릭 **확인**합니다.
4. Hello에 다시 **디스크** 블레이드에서 클릭 **저장** tooadd hello 디스크 toohello VM 구성 합니다.


### <a name="initialize-a-new-data-disk"></a>새 데이터 디스크 초기화

1. Toohello 가상 컴퓨터를 연결 합니다. 자세한 내용은 [어떻게 tooconnect 로그온 tooan Azure 가상 컴퓨터 및 Windows를 실행](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.
1. Hello 클릭 **시작** hello VM 및 형식 내부 메뉴 **diskmgmt.msc** 적중 및 **Enter**합니다. Hello 디스크 관리 스냅인 시작 됩니다.
2. 디스크 관리 새, 초기화 되지 않은 디스크 hello 디스크 초기화 창이 팝업 됩니다 인식 합니다.
3. Hello 새 디스크가 선택 되어 있는지 확인 하 고 클릭 **확인** tooinitialize 것입니다.
4. hello 새 디스크로 나타납니다으로 **할당 되지 않은**합니다. Hello 디스크에서 아무 곳 이나 마우스 오른쪽 단추로 클릭 하 고 선택 **새 단순 볼륨**합니다. hello **새 단순 볼륨 마법사** 시작 합니다.
5. 선택 작업이 완료 되 면 hello 기본값을 유지 하는 hello 마법사를 통해 이동 **마침**합니다.
6. 디스크 관리를 닫습니다.
7. 있는 팝업 하 게 사용 하려면 먼저 tooformat hello에 대 한 새 디스크가 필요 합니다. **디스크 포맷**을 클릭합니다.
8. Hello에 **새 디스크를 포맷** 검사 hello 설정, 클릭 한 다음 대화 상자, **시작**합니다.
9. 경고가 있는지 hello 데이터를 모두 지웁니다 hello 디스크 포맷, 클릭 **확인**합니다.
10. Hello 포맷이 완료 되 면 클릭 **확인**합니다.


## <a name="option-2-attach-an-existing-disk"></a>옵션 2: 기존 디스크 연결
1. Hello에 **디스크** 블레이드에서 클릭 **+ 추가 데이터 디스크**합니다.
2. Hello에 **연결 관리 되지 않는 디스크** 블레이드, **소스 형식** 선택 **기존 blob**합니다.

    ![디스크 설정 검토](./media/attach-disk-portal/attach-existing-unmanaged.png)

    3. 클릭 **찾아보기** toonavigate toohello 저장소 계정 및 컨테이너 hello 기존 VHD의 위치입니다. 클릭 하 고 VHD hello 한 다음 클릭 **선택**합니다.
4. 클릭 **확인** hello에 **연결 관리 되지 않는 디스크** 블레이드입니다.
5. Hello에 **디스크** 블레이드에서 클릭 **저장** hello VM tooadd hello 디스크 toohello 구성 합니다.
   


## <a name="use-trim-with-standard-storage"></a>표준 저장소와 TRIM 사용

표준 저장소(HDD)를 사용하는 경우 TRIM을 사용하도록 설정해야 합니다. TRIM 실제로 사용 하는 저장소에 대 한만 청구 됩니다 하므로 hello 디스크에 사용 하지 않는 블록을 삭제 합니다. 큰 파일을 만들고 삭제하는 경우 비용을 절감할 수 있습니다. 

이 명령은 toocheck hello 트림 설정을 실행할 수 있습니다. Windows VM에서 명령 프롬프트를 열어 다음을 입력합니다.

```
fsutil behavior query DisableDeleteNotify
```

Hello 명령이 0을 반환 하는 경우 TRIM 올바르게 활성화 됩니다. 1을 반환 하는 경우 다음 명령을 tooenable TRIM hello를 실행 합니다.
```
fsutil behavior set DisableDeleteNotify 0
```

디스크에서 데이터를 삭제 한 후 TRIM으로 조각 모음 hello 자르기 작업을 실행 하 여 제대로 플러시 되도록 할 수 있습니다.

```
defrag.exe <volume:> -l
```

Hello 볼륨을 포맷 하 여 hello 전체 볼륨을 잘라내는 보장할 수 있습니다.


## <a name="next-steps"></a>다음 단계
응용 프로그램에 toouse hello d: 드라이브 toostore 데이터가 필요 하면 [hello Windows 임시 디스크의 드라이브 문자 hello 변경](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.

