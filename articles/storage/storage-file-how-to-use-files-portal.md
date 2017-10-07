---
title: "aaaHow toomanage hello Azure 포털에서에서 Azure 파일 저장소 | Microsoft Docs"
description: "Toouse hello Azure 포털 toomanage Azure 파일 저장소에 알아봅니다."
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 385b99ac1c3d97ca79059ae8229afb53f1e825cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-file-storage-from-hello-azure-portal"></a>Toouse Azure 파일 저장소에서 Azure 포털을 hello 하는 방법
hello [Azure 포털](https://portal.azure.com) Azure 파일 저장소 관리를 위한 사용자 인터페이스를 제공 합니다. 웹 브라우저에서 작업을 수행 하는 hello를 수행할 수 있습니다.

* 파일 공유 만들기
* 업로드 한 파일 tooand 파일 공유에서 다운로드 합니다.
* 각 파일 공유의 hello 실제 사용을 모니터링 합니다.
* Hello 파일 공유 크기 할당량을 조정 합니다.
* Windows 또는 Linux 클라이언트에서 파일을 공유 하는 hello 탑재 명령을 toouse toomount를 복사 합니다.

## <a name="create-file-share"></a>파일 공유 만들기
1. Azure 포털 toohello에 로그인 합니다.
2. Hello 탐색 메뉴에서 클릭 **저장소 계정은** 또는 **저장소 계정 (클래식)**합니다.
    
    ![Hello 포털에서 toocreate 파일을 공유 하는 방법을 보여 주는 스크린샷](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share1.png)

3. 저장소 계정 선택

    ![Hello 포털에서 toocreate 파일을 공유 하는 방법을 보여 주는 스크린샷](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share2.png)

4. "파일" 서비스를 선택합니다.

    ![Hello 포털에서 toocreate 파일을 공유 하는 방법을 보여 주는 스크린샷](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share3.png)

5. "파일 공유"를 클릭 하 고 첫 번째 파일을 공유 하는 hello 링크 toocreate를 수행 합니다.

    ![Hello 포털에서 toocreate 파일을 공유 하는 방법을 보여 주는 스크린샷](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share4.png)

6. Hello 파일 공유 이름 및 입력 파일 (too5120 GB)를 공유 toocreate hello의 hello 크기 첫 번째 파일 공유 합니다. Hello 파일 공유를 만든 후에 SMB 2.1 또는 SMB 3.0을 지 원하는 모든 파일 시스템에서 탑재할 수 있습니다. 클릭할 수 **할당량** too5120 GB hello 파일의 hello 파일 공유 toochange hello 크기에 있습니다. 너무를 참조 하십시오[Azure 가격 계산기](https://azure.microsoft.com/pricing/calculator/) tooestimate hello 저장 비용은 Azure 파일 저장소를 사용 합니다.

    ![Hello 포털에서 toocreate 파일을 공유 하는 방법을 보여 주는 스크린샷](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share5.png)

## <a name="upload-and-download-files"></a>파일 업로드 및 다운로드
1. 이미 만든 파일 공유 중 하나를 선택합니다.

    ![파일을 다운로드 하 고 tooupload 포털 hello 하는 방법을 보여 주는 스크린샷](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file1.png)

2. 클릭 **업로드** 파일 업로드에 대 한 hello 사용자 인터페이스를 열려면 합니다.

    ![Hello 포털에서 tooupload 파일 하는 방법을 보여 주는 스크린샷](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file2.png)

## <a name="connect-toofile-share"></a>Toofile 공유를 연결 합니다.
-  클릭 **연결** 탑재 hello 파일 공유에 대 한 Windows 및 Linux에서 hello 명령줄을 가져올 수 있습니다. Linux 사용자를 참조할 수도 있습니다 너무[어떻게 toouse Azure 파일 저장소와 Linux](storage-how-to-use-files-linux.md) 다른 Linux 배포판에 대 한 자세한 설치 지침에 대 한 합니다.

    ![Toomount 파일 공유를 hello 하는 방법을 보여 주는 스크린샷](media/storage-file-how-to-use-files-portal/use-files-portal-connect.png)
-  파일을 탑재 명령은 Windows 또는 Linux에서 공유 하 고 Azure VM 또는 온-프레미스 컴퓨터에서 실행할 hello를 복사할 수 있습니다.

    ![Windows 및 Linux 용 hello 탑재 명령을 보여 주는 스크린샷](media/storage-file-how-to-use-files-portal/use-files-portal-show-mount-commands.png)

**팁:**  
toofind hello 저장소 계정 액세스 키를 탑재에 대 한 클릭 **이 저장소 계정에 대 한 보기 액세스 키** hello hello 맨 아래에 연결 페이지입니다.

## <a name="see-also"></a>참고 항목
Azure 파일 저장소에 대한 자세한 내용은 다음 링크를 참조합니다.

* [FAQ](storage-files-faq.md)
* [문제 해결](storage-troubleshoot-file-connection-problems.md)