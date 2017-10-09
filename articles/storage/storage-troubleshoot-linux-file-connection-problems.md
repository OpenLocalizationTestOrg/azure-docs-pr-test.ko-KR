---
title: "Linux에서 aaaTroubleshoot Azure 파일 저장소 문제 | Microsoft Docs"
description: "Linux에서 Azure File Storage 문제 해결"
services: storage
documentationcenter: 
author: genlin
manager: willchen
editor: na
tags: storage
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: genli
ms.openlocfilehash: 3dc537d714244451a5ff8e01f4a27f03873cf2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-linux"></a>Linux에서 Azure File Storage 문제 해결

이 문서에서는 Azure 파일 저장소 관련된 tooMicrosoft Linux 클라이언트에서 연결 된 일반적인 문제를 나열 합니다. 또한 이러한 문제의 가능한 원인과 해결 방법을 제공합니다.

<a id="permissiondenied"></a>
## <a name="permission-denied-disk-quota-exceeded-when-you-try-tooopen-a-file"></a>"[사용 권한이 거부 되었습니다] 디스크 할당량이 초과 되었습니다" tooopen 파일을 시도할 때

Linux에서 hello 다음과 유사한 오류 메시지가 나타날 수 있습니다.

**<filename> [사용 권한 거부됨] 디스크 할당량이 초과됨**

### <a name="cause"></a>원인

파일에 허용 되는 동시 열려 있는 핸들의 hello 상한값에 도달 했습니다.

### <a name="solution"></a>해결 방법

일부 핸들을 닫아 hello 동시 열려 있는 핸들 수를 줄인 hello 작업을 다시 시도 하십시오. 자세한 내용은 [Microsoft Azure Storage 성능 및 확장성 검사 목록](storage-performance-checklist.md)을 참조하세요.

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-linux"></a>Linux에서 Azure 파일 저장소에서 tooand를 복사 하는 느린 파일

-   특정 최소 I/O 크기 요구 사항이 없다면 최적의 성능을 위해 I/O 크기 hello으로 1MB를 사용 하는 것이 좋습니다.
-   다음 설정 hello 파일 크기는 확장을 쓸 때마다 만드는 대신 미리 쓰기를 사용 하 여 확장 하는 파일의 hello 최종 크기를 알고 있는 경우 소프트웨어 hello 파일에는 기록 되지 않은 꼬리에 0을 포함 하는 경우 호환성 문제가 발생 하지 않습니다 작성 합니다.
-   Hello 오른쪽 복사 방법을 사용 합니다.
    -   두 파일 공유 간의 전송에는 [AzCopy](storage-use-azcopy.md#file-copy)를 사용합니다.
    -   온-프레미스 컴퓨터와 파일 공유 간에는 [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/)를 사용합니다.

<a id="error112"></a>
## <a name="mount-error112-host-is-down-because-of-a-reconnection-time-out"></a>다시 연결 시간 제한으로 인한 "탑재 오류(112): 호스트가 중단됨"

클라이언트 hello 오랜 시간 동안 유휴 상태 였 "112" 탑재 오류가 hello Linux 클라이언트에서 발생 합니다. 확장 된 유휴 시간 후 hello 클라이언트의 연결이 끊어지고 hello 연결 시간이 초과 합니다.  

### <a name="cause"></a>원인

hello 연결 이유 뒤 hello에 대 한 유휴 상태가 될 수 있습니다.

-   Hello 기본 탑재 "소프트" 옵션을 사용 하는 경우 TCP 연결 toohello 서버를 다시 설정 방해 하는 네트워크 통신 오류
-   이전 커널에 존재하지 않는 최근 재연결 수정

### <a name="solution"></a>해결 방법

Hello Linux 커널에서이 다시 연결 문제 hello 변경 뒤의 일환으로 고정 됩니다.

- [수정 프로그램 toonot 다시 연결 smb3 세션 연기 소켓 다시 연결 후에 오랜 시간이 다시 연결](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93)
-   [소켓 재연결 직후 에코 서비스 호출](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7)
-   [CIFS: 재연결 동안 가능한 메모리 손상 수정](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b)
-   [CIFS: 재연결 동안 가능한 뮤텍스 이중 잠금 해결(커널 v4.9 이상)](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183)

그러나 이러한 변경 내용은 tooall hello Linux 배포판 아직 이식할 하지 수도 있습니다. 이 문제를이 수정 하 고 다른 재연결 수정 내용이 인기 있는 Linux 커널을 다음 hello: 4.4.40, 4.8.16, 및 4.9.1 합니다. 이 문제를이 수정 tooone 이러한 권장된 커널 버전을 업그레이드 하 여 얻을 수 있습니다.

### <a name="workaround"></a>해결 방법

하드 탑재를 지정하여 이 문제를 해결할 수 있습니다. 이렇게 하면 연결 될 때까지 또는 명시적으로 중단 되 고 네트워크 제한 시간 때문에 사용 되는 tooprevent 오류가 발생할 수 있습니다 때까지 hello 클라이언트 toowait 됩니다. 그러나 이 해결 방법은 무한 대기를 일으킬 수 있습니다. 필요에 따라 준비 된 toostop 연결이 유지 합니다.

Toohello 최신 커널 버전으로 업그레이드할 수 없는 경우 hello Azure 파일 공유를 작성 하는 tooevery 30 초 이하로 파일을 유지 하 여이 문제를 해결할 수 있습니다. 예: hello를 다시 작성에서 만들어지거나 수정 날짜 hello 파일 쓰기 작업 이어야 합니다. 그렇지 않은 경우 캐시 된 결과 얻을 수 있습니다 및 작업 hello 재연결을 트리거하지 않습니다 수 있습니다.

<a id="error115"></a>
## <a name="mount-error115-operation-now-in-progress-when-you-mount-azure-file-storage-by-using-smb-30"></a>SMB 3.0을 사용하여 Azure File Storage를 탑재할 때 "탑재 오류(115): 현재 작업 진행 중"

### <a name="cause"></a>원인

일부 Linux 배포판을 지원 하지 않는 암호화 기능 SMB 3.0에서 및 toomount Azure 파일 저장소 누락 된 기능으로 인해 SMB 3.0을 사용 하 여 시도 하는 경우 사용자가 "115" 오류 메시지가 표시 될 수 있습니다.

### <a name="solution"></a>해결 방법

Linux용 SMB 3.0에 대한 암호화 기능이 4.11 커널에 도입되었습니다. 이 기능을 사용하면 온-프레미스 또는 다른 Azure 지역에서 Azure 파일 공유를 탑재할 수 있습니다. 게시의 hello 시이 기능은 backported tooUbuntu 17.04 및 Ubuntu 16.10 되었습니다. Linux SMB 클라이언트에서 암호화를 지원 하지 않는 경우 SMB 2.1에 있는 Azure Linux VM에서 사용 하 여 Azure 파일 저장소를 탑재할 hello 파일 저장소 계정으로 동일한 데이터 센터 hello 합니다.

<a id="slowperformance"></a>
## <a name="slow-performance-on-an-azure-file-share-mounted-on-a-linux-vm"></a>Linux VM에 탑재된 Azure 파일 공유의 성능 저하

### <a name="cause"></a>원인

성능 저하의 한 가지 가능한 원인은 캐싱 비활성화입니다.

### <a name="solution"></a>해결 방법

toocheck 캐싱을 비활성화할지 여부를 찾습니다 hello **캐시 =** 항목입니다. 

**cache=none**은 캐싱이 비활성화되었음을 나타냅니다.  Hello 기본 탑재 명령을 사용 하 여 또는 hello를 명시적으로 추가 하 여 다시 탑재 hello 공유 **캐시 strict =** 옵션 toohello 탑재 명령 tooensure 기본 캐싱 캐싱 또는 "strict" 모드를 사용 하도록 설정 합니다.

일부 시나리오에서는 hello **serverino** 마운트 옵션으로 지정 하면 hello **ls** 모든 디렉터리 항목에 대 한 명령 toorun stat 합니다. 이러한 동작은 큰 디렉터리를 나열하는 경우 성능 저하를 일으킬 수 있습니다. Hello 마운트 옵션에서 확인할 수 있습니다 프로그램 **/등/fstab** 항목:

`//azureuser.file.core.windows.net/cifs /cifs cifs vers=3.0,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

Hello를 실행 하 여 hello 올바른 옵션은 사용 중인지 여부를 확인할 수도 있습니다 **sudo 탑재 | grep cifs** 명령과 같은 예제 출력이 다음 hello 해당 출력을 검사 합니다.

`//mabiccacifs.file.core.windows.net/cifs on /cifs type cifs (rw,relatime,vers=3.0,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777, dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

경우 hello **캐시 strict =** 또는 **serverino** 옵션은 하지 제공 탑재 해제 하 고 hello에서 hello mount 명령을 실행 하 여 Azure 파일 저장소를 다시 탑재 [설명서](storage-how-to-use-files-linux.md)합니다. 그런 다음 해당 hello 다시 검사 **/등/fstab** 항목에 올바른 hello 옵션입니다.

<a id="timestampslost"></a>
## <a name="time-stamps-were-lost-in-copying-files-from-windows-toolinux"></a>Windows tooLinux에서 파일 복사에 손실 된 타임 스탬프

Linux/Unix 플랫폼 hello **cp-p** 파일 1 및 2 파일 다른 사용자가 소유 하는 경우 명령이 실패 합니다.

### <a name="cause"></a>원인

force 플래그가 hello **f** COPYFILE 실행 결과 **cp-p-f** unix 합니다. 이 명령은 소유 하지 않은 hello 파일의 toopreserve hello 타임 스탬프에도 작동 하지 않습니다.

### <a name="workaround"></a>해결 방법

Hello 파일 복사 하기 위한 hello 저장소 계정 사용자를 사용 합니다.

- `Useadd : [storage account name]`
- `Passwd [storage account name]`
- `Su [storage account name]`
- `Cp -p filename.txt /share`

## <a name="need-help-contact-support"></a>도움이 필요하세요? 지원에 문의하세요.

도움이 필요 하면 여전히 필요 하면 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget 문제가 해결 신속 하 게 합니다.
