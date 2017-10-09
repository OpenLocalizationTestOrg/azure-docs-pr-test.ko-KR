---
title: "VM 데이터 디스크의 d: 드라이브 hello 확인 | Microsoft Docs"
description: "데이터 드라이브로 hello d: 드라이브를 사용할 수 있도록 toochange 드라이브는 Windows VM에 대 한 문자가 방법을 설명 합니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 0867a931-0055-4e31-8403-9b38a3eeb904
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: cynthn
ms.openlocfilehash: 43939da1a890ac4049266487951e3889aa0ed9d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-d-drive-as-a-data-drive-on-a-windows-vm"></a>Windows VM에서 데이터 드라이브로 hello d: 드라이브를 사용 하 여
응용 프로그램 toouse hello D 드라이브 toostore 데이터를 필요한 경우 이러한 지침 toouse hello 임시 디스크에 대 한 다른 드라이브 문자를 따릅니다. Tookeep 해야 하는 hello 임시 디스크 toostore 데이터를 사용 하지 마십시오.

크기를 조정 하면 또는 **중지 (할당 취소)** 가상 컴퓨터이 hello 가상 컴퓨터 tooa 새 하이퍼바이저의 배치를 트리거할 수 있습니다. 계획되거나 계획되지 않은 유지 관리 이벤트로 이 배치가 트리거될 수도 있습니다. 이 시나리오에서는 hello 임시 디스크에 다시 할당 된 toohello 첫 번째 사용 가능한 드라이브 문자가 됩니다. 특히 hello d: 드라이브를 필요로 하는 응용 프로그램의 경우 이러한 단계 tootemporarily 이동 hello pagefile.sys, 새 데이터 디스크를 연결 하 고 D hello 문자를 할당 한 다음 toohello 임시 드라이브를 다시 이동 hello pagefile.sys toofollow 필요 합니다. 완료 되 면 Azure 사항을 다시 hello d: hello VM tooa 다른 하이퍼바이저를 이동 하는 경우.

Azure hello 임시 디스크를 사용 하는 방법에 대 한 자세한 내용은 참조 [hello 임시 드라이브를 Microsoft Azure 가상 컴퓨터 이해](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)

## <a name="attach-hello-data-disk"></a>Hello 데이터 디스크 연결
첫째, tooattach hello 데이터 디스크 toohello 가상 컴퓨터 필요 합니다. toodo이 hello 포털을 사용 하 여, 참조 [tooattach 관리 되는 데이터 디스크 hello Azure 포털에에서 어떻게](attach-managed-disk-portal.md)합니다.

## <a name="temporarily-move-pagefilesys-tooc-drive"></a>Pagefile.sys tooC 드라이브를 일시적으로 이동
1. Toohello 가상 컴퓨터를 연결 합니다. 
2. 마우스 오른쪽 단추로 클릭 hello **시작** 메뉴와 선택 **시스템**합니다.
3. Hello 왼쪽 메뉴에서 선택 **고급 시스템 설정**합니다.
4. Hello에 **성능** 섹션에서 **설정을**합니다.
5. 선택 hello **고급** 탭 합니다.
6. Hello에 **가상 메모리** 섹션에서 **변경**합니다.
7. 선택 hello **C** 드라이브 및 클릭 **시스템 관리 하는 크기** 클릭 하 고 **설정**합니다.
8. 선택 hello **D** 드라이브 및 클릭 **페이징 파일 없음** 클릭 하 고 **설정**합니다.
9. 적용을 클릭합니다. 해당 hello 컴퓨터 toobe hello 변경 tootake 영향에 대 한 다시 시작 필요 경고를 받아볼 수 있습니다.
10. Hello 가상 컴퓨터를 다시 시작 합니다.

## <a name="change-hello-drive-letters"></a>Hello 드라이브 문자 변경
1. 한 번 hello VM 다시 시작 하면 toohello VM에 다시 로그온 합니다.
2. Hello 클릭 **시작** 메뉴 및 형식 **diskmgmt.msc** Enter 키를 누릅니다. 디스크 관리가 시작됩니다.
3. 마우스 오른쪽 단추로 클릭 **D**, 임시 저장소 드라이브 hello 및 선택 **드라이브 문자 및 경로 변경**합니다.
4. 드라이브 문자에서 **T**와 같은 새 드라이브를 선택한 후 **확인**을 클릭합니다. 
5. Hello 데이터 디스크를 마우스 오른쪽 단추로 클릭 하 고 선택 **드라이브 문자 및 경로 변경**합니다.
6. 드라이브 문자에서 드라이브 **D**를 선택한 후 **확인**을 클릭합니다. 

## <a name="move-pagefilesys-back-toohello-temporary-storage-drive"></a>Pagefile.sys 백 toohello 임시 저장소 드라이브를 이동 합니다.
1. 마우스 오른쪽 단추로 클릭 hello **시작** 메뉴와 선택 **시스템**
2. Hello 왼쪽 메뉴에서 선택 **고급 시스템 설정**합니다.
3. Hello에 **성능** 섹션에서 **설정을**합니다.
4. 선택 hello **고급** 탭 합니다.
5. Hello에 **가상 메모리** 섹션에서 **변경**합니다.
6. Hello 운영 체제 드라이브를 선택 **C** 클릭 **페이징 파일 없음** 클릭 하 고 **설정**합니다.
7. Hello 임시 저장소 드라이브를 선택 **T** 클릭 하 고 **시스템 관리 하는 크기** 클릭 하 고 **설정**합니다.
8. **Apply**를 클릭합니다. 해당 hello 컴퓨터 toobe hello 변경 tootake 영향에 대 한 다시 시작 필요 경고를 받아볼 수 있습니다.
9. Hello 가상 컴퓨터를 다시 시작 합니다.

## <a name="next-steps"></a>다음 단계
* Hello 하 여 사용 가능한 tooyour 가상 컴퓨터 저장소를 늘릴 수 [추가 데이터 디스크 연결](attach-managed-disk-portal.md)합니다.

