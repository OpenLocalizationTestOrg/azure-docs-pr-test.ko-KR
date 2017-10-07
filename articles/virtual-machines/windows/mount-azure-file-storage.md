---
title: "Windows Azure VM에서 Azure 파일 저장소 aaaMount | Microsoft Docs"
description: "Hello 클라우드 Azure 파일 저장소에 파일을 저장 하 고 Azure 가상 컴퓨터 (VM)에서 클라우드 파일 공유를 탑재 합니다."
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: 
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 965f1c1b3f0d07fec6d86f9312a05e02e8ce7fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-shares-with-windows-vms"></a>Windows VM과 Azure 파일 공유 사용 

Vm에서 방법은 toostore 및 액세스 파일로 Azure 파일 공유를 사용할 수 있습니다. 예를 들어 스크립트 또는 프로그램의 모든 Vm tooshare 되도록 응용 프로그램 구성 파일을 저장할 수 있습니다. 이 항목에서는 보여줍니다 toocreate 및 탑재 Azure 파일 공유, 방법 등에 tooupload 파일과 다운로드 합니다.

## <a name="connect-tooa-file-share-from-a-vm"></a>VM에서 tooa 파일 공유에 연결

이 섹션에서는 파일을 tooconnect 원하는 공유를 이미 있으면 가정 합니다. 하나는 toocreate 필요한 경우 참조 [파일 공유 만들기](#create-a-file-share) 이 항목의 뒷부분에 나오는 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 왼쪽된 메뉴에서 클릭 **저장소 계정은**합니다.
3. 저장소 계정 선택
4. Hello에 **개요** 페이지의 **서비스**선택, **파일**합니다.
5. 파일 공유를 선택합니다.
6. 클릭 **연결** tooopen Windows 또는 Linux에서 탑재 hello 파일 공유에 대 한 hello 명령줄 구문을 보여 주는 페이지입니다.
7. Hello 명령 구문을 hello를 강조 표시 하 고 메모장 이나 다른 쉽게 액세스할 수 있는 순서에 붙여 넣습니다. 
8. Hello 구문 tooremove hello 앞에 오는 편집 * * > * * 및 바꾸기 *[드라이브 문자]* hello 드라이브 문자 (예를 들어 **y:**) 넣을 toomount hello 파일 공유 합니다.
8. Tooyour VM을 연결 하 고 명령 프롬프트를 엽니다.
9. Hello에 붙여넣기 연결 구문을 편집 하 고 적중 **Enter**합니다.
10. Hello 연결을 만들면 메시지가 hello **hello 명령이 성공적으로 완료 합니다.**
11. Hello 드라이브 문자 tooswitch toothat 드라이브에 입력 하 여 hello 연결을 확인 한 다음 입력 **dir** hello 파일 공유의 toosee hello 내용입니다.



## <a name="create-a-file-share"></a>파일 공유 만들기 
1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 왼쪽된 메뉴에서 클릭 **저장소 계정은**합니다.
3. 저장소 계정 선택
4. Hello에 **개요** 페이지의 **서비스**선택, **파일**합니다.
5. Hello 파일 서비스 페이지에서 클릭 **+ 파일 공유** toocreate 첫 번째 파일을 공유 합니다. \ \
6. Hello 파일 공유 이름을 입력 합니다. 파일 공유 이름은 소문자, 숫자 및 단일 하이픈을 사용할 수 있습니다. hello 이름은 하이픈으로 시작할 수 없습니다 및 여러를 사용할 수 없는 연속 된 하이픈입니다. 
7. Hello 파일 크기에서 제한에 대 한 채우기 too5120 GB를 수 있습니다.
8. 클릭 **확인** toodeploy hello 파일 공유 합니다.
   
## <a name="upload-files"></a>파일 업로드
1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 왼쪽된 메뉴에서 클릭 **저장소 계정은**합니다.
3. 저장소 계정 선택
4. Hello에 **개요** 페이지의 **서비스**선택, **파일**합니다.
5. 파일 공유를 선택합니다.
6. 클릭 **업로드** tooopen hello **파일 업로드** 페이지.
7. Hello 폴더 아이콘 toobrowse 로컬 파일 시스템 파일 tooupload 클릭 합니다.   
8. 클릭 **업로드** tooupload hello 파일 toohello 파일 공유 합니다.

## <a name="download-files"></a>파일 다운로드
1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 왼쪽된 메뉴에서 클릭 **저장소 계정은**합니다.
3. 저장소 계정 선택
4. Hello에 **개요** 페이지의 **서비스**선택, **파일**합니다.
5. 파일 공유를 선택합니다.
6. Hello 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 **다운로드** toodownload 것 tooyour 로컬 컴퓨터입니다.
   

## <a name="next-steps"></a>다음 단계

또한 PowerShell을 사용하여 파일 공유를 만들고 관리할 수 있습니다. 자세한 내용은 [Windows에서 Azure File storage 시작](../../storage/files/storage-dotnet-how-to-use-files.md)을 참조하세요.
