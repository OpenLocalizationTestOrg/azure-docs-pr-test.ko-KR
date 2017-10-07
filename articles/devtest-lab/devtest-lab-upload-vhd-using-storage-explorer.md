---
title: "aaaUpload VHD 파일을 Microsoft Azure 저장소 탐색기를 사용 하 여 tooAzure DevTest Labs | Microsoft Docs"
description: "Microsoft Azure 저장소 탐색기를 사용 하 여 VHD 파일 toolab 저장소 계정에 업로드"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 686691e3676cea4b2d7cd8bf045bc43a792c667e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-microsoft-azure-storage-explorer"></a>Microsoft Azure 저장소 탐색기를 사용 하 여 VHD 파일 toolab 저장소 계정에 업로드

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

Azure DevTest Labs, VHD 파일 tooprovision 사용 되는 가상 컴퓨터는 사용자 지정 이미지를 사용 하는 toocreate 될 수 있습니다. 이 문서에서는 설명 방법을 toouse [Microsoft Azure 저장소 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooupload VHD 파일 tooa 랩 저장소 계정입니다. VHD 파일을 업로드 한 후 hello [다음 단계 섹션](#next-steps) toocreate hello에서 사용자 지정 이미지를 VHD 파일을 업로드 하는 방법을 보여 주는 몇 가지 기사를 나열 합니다. Azure의 디스크 및 VHD에 대한 자세한 내용은 [가상 컴퓨터용 디스크 및 VHD 정보](../virtual-machines/linux/about-disks-and-vhds.md)를 참조하세요.

## <a name="step-by-step-instructions"></a>단계별 지침

다음 단계 워크 tooDevTest Labs를 사용 하 여 파일을 VHD를 업로드 하는 과정를 hello [Microsoft Azure 저장소 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md)합니다.

1. [다운로드 및 설치 hello 최신 버전의 Microsoft Azure 저장소 탐색기 hello](http://www.storageexplorer.com)합니다.

1. Hello hello 랩 저장소 계정의 이름으로 hello Azure 포털을 사용 하 여 가져오기:

    1. Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.
    
    1. 선택 **더 많은 서비스**를 선택한 후 **DevTest Labs** hello 목록에서 합니다.
    
    1. 랩의 hello 목록에서 원하는 랩 hello를 선택 합니다.  
    
    1. Hello 랩 블레이드에서 선택 **구성**합니다. 
    
    1. Hello 랩에 **구성** 블레이드를 **사용자 지정 이미지 (Vhd)**합니다.
    
    1. Hello에 **사용자 지정 이미지** 블레이드에서 선택 **+ 추가**합니다. 
    
    1. Hello에 **사용자 지정 이미지** 블레이드를 **VHD**합니다.
    
    1. Hello에 **VHD** 블레이드를 **PowerShell을 사용 하 여 VHD 업로드**합니다.
    
        ![PowerShell을 사용하여 VHD 업로드][0]
    
    1. hello **PowerShell을 사용 하 여 이미지를 업로드** 블레이드 표시 호출 toohello **Add-azurevhd** cmdlet. 첫 번째 매개 변수를 hello (*대상*) 형식에 따라 hello에 hello 랩에 대 한 hello 저장소 계정 이름을 포함 합니다.
    
        https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/... 

    1. 이후 단계에서 사용 중 이므로 저장소 계정 이름을 hello 기록해 둡니다.
    
1. Tooan 저장소 탐색기를 사용 하 여 Azure 구독 계정에 연결 합니다.

    > [!TIP] 
    > 
    > 저장소 탐색기는 여러 가지 연결 옵션을 지원합니다. 이 섹션에서는 Azure 구독에 연결 된 연결 tooa 저장소 계정을 보여 줍니다. toosee hello 저장소 탐색기에서 지 원하는 다른 연결 옵션, toohello 문서 참조 [저장소 탐색기 시작](../vs-azure-tools-storage-manage-with-storage-explorer.md)합니다.
 
    1. 저장소 탐색기를 엽니다.
    
    1. 저장소 탐색기에서 **Azure 계정 설정**을 선택합니다. 
    
        ![Azure 계정 설정][1]
    
    1. hello 왼쪽된 창에는 hello Microsoft 계정에 로그인 한 경우 표시 됩니다. 선택 tooconnect tooanother 계정 **계정 추가**, 하나 이상의 활성 Azure 구독에 연관 된 Microsoft 계정 사용 하 여 대화 상자 toosign hello를 따릅니다.
    
        ![계정 추가][2]
    
    1. Microsoft 계정으로 성공적으로 로그인 되 면 hello 왼쪽된 창의 해당 계정과 연결 된 Azure 구독의 hello로 채웁니다. 선택 된 toowork, 한 다음 선택 하는 Azure 구독 hello **적용**합니다. (선택 **모든 구독** 전환 합니다. 모든 선택을 hello 또는 Azure 구독을 나열 없는 hello.)
    
        ![Azure 구독 선택][3]
    
    1. hello 왼쪽된 창에 선택한 hello Azure 구독과 연결 된 hello 저장소 계정을 표시 됩니다.
    
        ![선택한 Azure 구독][4]

1. Hello 랩 저장소 계정을 찾습니다.

    1. Hello 저장소 탐색기 왼쪽된 창에서 찾아 hello hello 랩 소유 하는 Azure 구독에 대 한 hello 노드를 확장 합니다.
    
    1. Hello 구독 노드를 확장 **저장소 계정은**합니다.

    1. 에 대 한 hello 랩 저장소 계정 노드 tooreveal 노드 확장 **Blob 컨테이너**, **파일 공유**, **큐**, 및 **테이블**합니다.
    
    1. Hello 확장 **Blob 컨테이너** 노드.
    
    1. Hello 오른쪽 창에서 hello 업로드 blob 컨테이너 toodisplay 콘텐츠를 선택 합니다.
        
        ![업로드 디렉터리][5]

1. 저장소 탐색기를 사용 하 여 hello VHD 파일을 업로드 합니다.

    1. Hello 저장소 탐색기 오른쪽 창에서 blob hello hello 목록이 표시 되어야 **업로드** hello 랩 저장소 계정의 blob 컨테이너입니다. Hello blob 편집기 도구 모음에서 선택 **업로드** 
        
        ![업로드 단추][6]
    
    1. Hello에서 **업로드** 드롭 다운 메뉴 **파일 업로드 중...** .
    
    1. Hello에 **파일 업로드** 대화 상자에서 선택 hello 줄임표 (...).
        
        ![파일 선택][8]  

    1. Hello에 **파일을 선택 tooupload** 대화 상자에서 찾아보기 toohello 원하는 VHD 파일을 선택한 다음 선택 **열려**합니다.
    
    1. 때 toohello 반환 **파일 업로드** 대화 상자에서 변경 **유형 Blob** 너무**페이지 Blob**합니다.
    
    1. **업로드**를 선택합니다.

        ![파일 선택][9]  
    
    1. 저장소 탐색기 hello **활동 로그** 링크 toocancel hello 업로드) (함께 hello 다운로드 상태 창에 표시 합니다. VHD 파일을 업로드할 hello 프로세스 hello VHD 파일의 hello 크기 및 연결 속도 따라 시간이 오래 걸릴 수 있습니다. 

        ![파일 업로드 상태][10]  

## <a name="next-steps"></a>다음 단계

- [Hello Azure 포털을 사용 하 여 VHD 파일에서 DevTest Labs를 Azure에서 사용자 지정 이미지 만들기](devtest-lab-create-template.md)
- [PowerShell을 사용하여 VHD 파일에서 Azure DevTest Labs에 사용자 지정 이미지 만들기](devtest-lab-create-custom-image-from-vhd-using-powershell.md)

[0]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-image-using-psh.png
[1]: ./media/devtest-lab-upload-vhd-using-storage-explorer/settings-icon.png
[2]: ./media/devtest-lab-upload-vhd-using-storage-explorer/add-account-link.png
[3]: ./media/devtest-lab-upload-vhd-using-storage-explorer/subscriptions-list.png
[4]: ./media/devtest-lab-upload-vhd-using-storage-explorer/storage-accounts-list.png
[5]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-dir.png
[6]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-button.png
[7]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-files.png
[8]: ./media/devtest-lab-upload-vhd-using-storage-explorer/select-file.png
[9]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-file.png
[10]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-status.png
