---
title: "Azure RemoteApp에 대 한 사용자 지정 이미지 aaaUpload | Microsoft Docs"
description: "어떻게 tooupload 사용자 지정 이미지를 Azure RemoteApp에 알아봅니다"
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: 299e0510-1a6b-4fdf-914a-3631b061a360
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: ericor
ms.openlocfilehash: 6ad40fe58795ece37f4c7900be01bc713938da87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-image-for-azure-remoteapp"></a>Azure RemoteApp에 대한 사용자 지정 이미지 업로드
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

이 변경 내용으로 업데이트 또는 사용자 지정 템플릿 이미지를 만든 해야 tooupload 해당 이미지 tooyour Azure RemoteApp 이미지 라이브러리입니다. 다음 단계를 사용합니다.

## <a name="before-you-start"></a>시작하기 전에
1. 사용자 지정 이미지 hello 충족 확인 [이미지 요구 사항](remoteapp-imagereqs.md) 및 [응용 프로그램 요구 사항](remoteapp-appreqs.md)합니다.
2. Hello 설치 [Azure PowerShell 모듈](/powershell/azure/overview)합니다.

## <a name="step-by-step-on-how-tooupload-custom-image"></a>방법에 대해 과정을 단계별로 tooupload 사용자 지정 이미지
1. Azure 관리 포털을 열고 toohello RemoteApp 페이지를 이동 합니다.
2. Hello에 **템플릿 이미지** 탭을 클릭 **업로드** hello hello 페이지 맨 아래에 있습니다.
3. 이미지에 대 한 이름을 입력 하 고 hello 저장소 계정 위치를 지정 합니다. Hello 위치는 hello 확인 RemoteApp 컬렉션이 나 하나 toocreate 저장할 위치와 같은 위치입니다.
4. 메시지가 표시 되 면 다운로드 hello 스크립트 tooyour 로컬 PC입니다.
5. Hello 명령 매개 변수 hello 텍스트 상자 tooyour 클립보드에 복사 합니다.
6. 관리자 권한 Windows PowerShell 창을 엽니다.
7. 관리자 권한 Windows PowerShell 창을 hello에서 toohello 이동 hello 스크립트를 다운로드 하는 동일한 디렉터리입니다.
8. 붙여넣기 hello 명령 및 키를 눌러 복사 **Enter**합니다.
   
   hello 업로드 프로세스 시작 되 고 기간 네트워크 속도 hello 이미지의 크기를 비롯 한 여러 요인에 따라 달라질 수 있습니다.
9. 업로드가 성공 하지 못하면 네트워크 중단 또는 작업으로 인해 그렇게 하는 경우 항상 hello 업로드 프로세스를 시작한 재개할 수 있습니다. hello 스크립트를 사용 하 여 다시 실행 하는 업로드 tooresume hello 동일 명령줄입니다.

> [!WARNING]
> Hello 업로드 스크립트를 수정 하지 마십시오. 특정 확인 이미지 충족 hello 이미지 요구 사항 및 응용 프로그램 요구 사항 hello 구현된 tooensure 되었습니다.
> 
> 

## <a name="common-problems"></a>일반적인 문제
* Azure PowerShell이 아닌 Windows PowerShell을 사용해야 합니다. Hello 업로드 프로세스 중 특정 모듈에 필요 하기 때문에 필요가 tooinstall hello Azure PowerShell 모듈입니다.
* Hello 스크립트 변경해 서는 안, 유효성 검사는 사용자 편의 위해 합니다.
* Hello vhd 파일 업로드 중 잠겨 가져옵니다 hello 파일을 복사 또는 tooa 새 위치 및 시도 업로드 다시 이동 합니다. 업로드를 방지하는 일부 Windows 프로세스가 있을 수 있습니다.  

