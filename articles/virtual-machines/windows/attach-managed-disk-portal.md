---
title: "관리 되는 데이터 디스크 tooa Windows VM-Azure aaaAttach | Microsoft Docs"
description: "새 tooattach 데이터 디스크 tooa를 관리 하는 방법은 Windows VM에 Azure 포털 사용 하 여 hello hello 리소스 관리자 배포 모델입니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: bacc0589ad2d93e4d3d055c8f837f8db27291ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-managed-data-disk-tooa-windows-vm-in-hello-azure-portal"></a>Tooattach 관리 되는 데이터 hello Azure 포털에서에서 tooa Windows VM 디스크 하는 방법

이 문서에서는 tooattach 새 관리 되는 데이터 hello Azure 포털을 통해 tooWindows 가상 컴퓨터 디스크 하는 방법을 설명 합니다. 이 작업을 수행 하기 전에 다음 팁을 검토하세요.

* hello 가상 컴퓨터의 hello 크기 첨부할 수 데이터 디스크 수를 제어 합니다. 자세한 내용은 [가상 컴퓨터의 크기](sizes.md)를 참조하세요.
* 새 디스크에 대 한 toocreate 필요 하지 않습니다 것 첫 번째 Azure가 연결 하는 경우 만들기 때문에 있습니다.

또한 [Powershell을 사용하여 데이터 디스크를 연결](attach-disk-ps.md)할 수 있습니다.



## <a name="add-a-data-disk"></a>데이터 디스크 추가
1. Hello hello 왼쪽 메뉴를 클릭 **가상 컴퓨터**합니다.
2. Hello 목록에서 hello 가상 컴퓨터를 선택 합니다.
3. Hello 가상 컴퓨터 블레이드 클릭 **디스크**합니다.
   4. Hello에 **디스크** 블레이드에서 클릭 **+ 추가 데이터 디스크**합니다.
5. Hello hello 새 디스크에 대 한 드롭다운 목록에서에서 선택 **빈 만들**합니다.
6. Hello에 **만들기 관리 되는 디스크** 블레이드에서 hello 디스크에 대 한 이름을 입력 하 고 조정 필요에 따라 다른 설정을 hello 합니다. 완료하면 **만들기**를 클릭합니다.
7. Hello에 **디스크** 블레이드에서 hello VM에 대 한 toosave hello 새 디스크 구성 저장을 클릭 합니다.
6. Azure hello 디스크를 만들고이 toohello 가상 컴퓨터 연결을 새 디스크 hello hello 가상 컴퓨터의 디스크 설정이 아래에 나열 됩니다 **데이터 디스크**합니다.


## <a name="initialize-a-new-data-disk"></a>새 데이터 디스크 초기화

1. Toohello VM을 연결 합니다.
1. Hello VM 내 hello 시작 메뉴를 클릭 하는 입력 **diskmgmt.msc** 적중 및 **Enter**합니다. Hello 디스크 관리 스냅인가 시작 됩니다.
2. 디스크 관리에서는 인식 새로운 초기화 되지 않은 디스크를 해야 하 고 hello 디스크 초기화 창이 팝업 됩니다.
3. Hello 새 디스크가 선택 되어 있는지 확인 하 고 클릭 **확인** tooinitialize 것입니다.
4. 새 디스크 hello로 표시 됩니다 **할당 되지 않은**합니다. Hello 디스크에서 아무 곳 이나 마우스 오른쪽 단추로 클릭 하 고 선택 **새 단순 볼륨**합니다. hello **새 단순 볼륨 마법사** 시작 됩니다.
5. 선택 작업이 완료 되 면 hello 기본값을 유지 하는 hello 마법사를 통해 이동 **마침**합니다.
6. 디스크 관리를 닫습니다.
7. 받아볼 수 팝업을 사용 하려면 먼저 tooformat hello에 대 한 새 디스크가 필요 합니다. **디스크 포맷**을 클릭합니다.
8. Hello에 **새 디스크를 포맷** 검사 hello 설정, 클릭 한 다음 대화 상자, **시작**합니다.
9. hello 디스크 포맷를 허무는 hello 데이터의 모든 경고를 받게 됩니다 클릭 **확인**합니다.
10. Hello 포맷이 완료 되 면 클릭 **확인**합니다.

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
