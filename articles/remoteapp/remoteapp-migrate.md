---
title: "Azure RemoteApp에서 사용자 데이터 aaaMigrate | Microsoft Docs"
description: "자세한 내용은 방법 toomigrate Azure RemoteApp에서 사용자 데이터입니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d7e4fbf1-cb42-4430-94a0-ed6d4676fc86
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: aefc6ccc2c6173754acf6cad06102f27c8cb1d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-data-into-and-out-of-azure-remoteapp"></a>방법 및 Azure RemoteApp 외부로 toomigrate 데이터
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

여러 다양 한 도구 및 tootransfer 메서드를 사용할 수 있습니다 [사용자 데이터](remoteapp-upd.md) 및 Azure RemoteApp 외부로 합니다. 몇 가지 방법은 다음과 같습니다.

* 클립보드 공유를 사용하여 복사 및 붙여넣기
* 파일 및 데이터 tooa 파일 서버에 복사
* 브라우저를 통해 비즈니스에 대 한 파일 tooOneDrive 복사
* 리디렉션을 사용하여 파일 복사

> [!NOTE]
> 동기화 에이전트-비즈니스 또는 소비자에 대 한 hello OneDrive를 사용할 수 없습니다 것 [는 지원 되지 않습니다](remoteapp-onedrive.md) Azure RemoteApp에서 합니다.
> 
> 

## <a name="use-copy-and-paste-in-file-explorer"></a>파일 탐색기에서 복사 및 붙여넣기 사용
복사 및 붙여넣기 hello 클립보드를 사용 하 여 RemoteApp 배포에서 활성화 되어 [기본적으로](remoteapp-redirection.md)합니다. 따라서 로컬 PC와 RemoteApp 앱 간에 파일을 복사할 수 있습니다. 종종 hello RemoteApp에 앱을 사용 하는 일반적인 과정을 통해 사용자가 저장 파일 tootheir Upd-데이터 RemoteApp에서 쉽게를 이동 합니다.

1. [파일 탐색기를 앱으로 게시](remoteapp-publish.md) 합니다. (이 작업은 관리 작업입니다.)
2. 직접 게시 하는 사용자가 toolaunch hello 파일 탐색기 앱 및 toouse 해당 toocopy 및 붙여넣기 파일의 UPD 및 옵트아웃 합니다.

## <a name="upload-files-and-data-tooa-file-server-by-using-standard-network-file-copy"></a>표준 네트워크 파일 복사를 사용 하 여 파일 및 tooa 파일 서버 데이터 업로드
조직에서는 자주 파일 서버 toostore 일반 데이터를 사용합니다. Hello 서버 이름이 나 위치를 알고 있는 사용자가 hello hello 서버에 대 한 로컬 네트워크 수 이동한 다음 위에 했다는 것 처럼, 파일을 복사 합니다. 다시 toopublish 파일 탐색기 tooRemoteApp 원하는 하 고 사용자와 공유 합니다.

> [!NOTE]
> hello 파일 서버는 RemoteApp에 배포 된 hello 라우팅할 수 있는 네트워크에 있어야 합니다.
> 
> 

## <a name="copy-files-tooonedrive-for-business"></a>비즈니스에 대 한 파일 tooOneDrive 복사
RemoteApp에서 비즈니스 동기화 에이전트에 대 한 hello OneDrive를 사용할 수 없습니다, 있지만 여전히 파일 복사할 수 있습니다 UPD tooOneDrive에서 비즈니스에 대 한 브라우저를 통해 합니다. 

1. 파일 탐색기 tooRemoteApp 게시 하 고 그런 다음 사용자가 tooaccess hello 이러한 앱을 통해 파일을 지시할 키를 누릅니다. 
2. 이므로 쉬운 tootransfer 파일을 압축 하는 경우 사용자 비즈니스에 대 한 hello 파일 toomove tooOneDrive 일부만 포함 하는.zip 파일을 만들어야 합니다.
3. 사용자가 toogo toohello Office 365 포털 및 묻고 tooOneDrive 이동 하 여 hello.zip 파일을 업로드 합니다.

## <a name="copy-files-by-using-drive-redirection"></a>드라이브 리디렉션을 사용하여 파일 복사
[드라이브 리디렉션](remoteapp-redirection.md)을 사용하도록 설정했으면 사용자에 대해 매핑된 드라이브를 이미 만들었을 것입니다. 이 경우 zip 파일에 리디렉션 hello 드라이브 수 및 다음 tootheir 저장 로컬 PC입니다.

## <a name="how-administrators-can-export-data"></a>관리자가 데이터를 내보내는 방법

관리 합니다. Azure RemoteApp에서 모든 사용자 프로필 디스크 (UPD)를 내보낼 수에 대 한 구독 tooAzure Azure PowerShell을 사용 하 여 저장소 내에서 모든 컬렉션에 대 한 내보내기 AzureRemoteAppUserDisk cmdlet.  없는 능력 tooselect 개별 UPD의 있습니다.  Hello PowerShell 명령을 실행 될 때 각 사용자 디스크의 고정된 디스크 크기가 50gb 되며 내보낸된 tooAzure 저장 되어야 합니다.  이 저장소에 대한 바로 Azure Storage 비용이 부과됩니다.  이 명령을 실행 하는 경우에 세션이 그렇지 않으면 hello 내보내기가 실패 합니다.

도메인에 가입된 Azure RemoteApp 배포에 대한 UPD는 RDS 배포에만 다시 사용될 수 있으며 도메인에 가입되지 않은 배포는 사용할 수 없습니다.  Toouse RDS 배포에서이 디스크를 사용할 경우 좋습니다 우리의 [스크립트 자동화 된](https://github.com/arcadiahlyy/aramigration) 내보내기, 변환을 UPD의 hello는 RDS 배포로 가져옵니다.

