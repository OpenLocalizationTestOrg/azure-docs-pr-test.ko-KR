---
title: "Azure 클라우드 셸에서 (미리 보기) aaaPersist 파일 | Microsoft Docs"
description: "Azure Cloud Shell에서 파일을 유지하는 방법의 연습입니다."
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: b230453d5551c545553d63559741950206e4f1b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="persist-files-in-azure-cloud-shell"></a>Azure Cloud Shell에서 파일 유지
클라우드 셸에서는 세션 전반에 걸쳐 Azure 파일 저장소 toopersist 파일 활용 합니다.

## <a name="set-up-a-clouddrive-file-share"></a>`clouddrive` 파일 공유 설정
처음 시작 시 클라우드 셸 묻는 메시지를 기존 또는 새 파일 공유를 통해 파일을 toopersist 세션 tooassociate 합니다.

### <a name="create-new-storage"></a>새 저장소 만들기

기본 설정을 사용 하 고만 구독을 선택 하는 경우 클라우드 셸 가장 tooyou 가까이 있는 hello 지원 영역에 사용자 대신 세 개의 리소스를 만듭니다.
* 리소스 그룹: `cloud-shell-storage-<region>`
* 저장소 계정: `cs<uniqueGuid>`
* 파일 공유: `cs-<user>-<domain>-com-<uniqueGuid>`

![hello 구독 설정](media/basic-storage.png)

hello 파일 공유로 탑재할 `clouddrive` 에 프로그램 `$Home` 디렉터리입니다. hello 파일 공유는도 자동으로 및에 대해 만들어지는 5GB 이미지를 업데이트 하 고 계속 되 면 사용 되는 toostore 프로그램 `$Home` 디렉터리입니다. 이 일회성 작업 이므로 이후의 세션 hello 파일 공유를 자동으로 탑재 합니다.

### <a name="use-existing-resources"></a>기존 리소스 사용

고급 옵션 hello를 사용 하 여 기존 리소스를 연결할 수 있습니다. Hello 저장소 설정 프롬프트가 나타나면 선택 **고급 설정 표시** tooview 추가 옵션입니다. 기존 파일 공유 5GB 사용자 이미지 toopersist 수신 프로그램 `$Home` 디렉터리입니다. 로컬 중복 및 지리적 중복 저장소 계정의 및 클라우드 셸 영역에 대 한 hello 드롭 다운 메뉴 필터링 됩니다.

![hello 리소스 그룹 설정](media/advanced-storage.png)

### <a name="restrict-resource-creation-with-an-azure-resource-policy"></a>Azure 리소스 정책으로 리소스 만들기 제한
Cloud Shell에서 생성된 저장소 계정에 `ms-resource-usage:azure-cloud-shell` 태그가 지정됩니다. 클라우드 셸에서 저장소 계정을 만들지 못하도록 toodisallow 사용자 만듭니다는 [태그에 대 한 Azure 리소스 정책](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) 이 특정 태그에 의해 트리거되는입니다.

## <a name="how-cloud-shell-works"></a>Cloud Shell 작동 방식
클라우드 셸 모두 hello 다음 메서드를 통해 파일을 유지 됩니다.
* 디스크 이미지를 만들어 프로그램 `$Home` hello 디렉터리 내에서 모든 디렉터리 toopersist 콘텐츠입니다. hello 디스크 이미지 사용자 지정 된 파일 공유에 저장 된 `acc_<User>.img` 에서 `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, 변경 내용을 자동으로 동기화 하 고 있습니다.

* 직접 파일 공유의 상호 작용을 위해 `$Home` 디렉터리에서 지정된 파일 공유를 `clouddrive`로 마운트합니다. `/Home/<User>/clouddrive`너무 매핑된`fileshare.storage.windows.net/fileshare`합니다.
 
> [!NOTE]
> SSH 키와 같이 `$Home` 디렉터리의 모든 파일은 마운트된 파일 공유에 저장된 사용자 디스크 이미지에서 유지됩니다. `$Home` 디렉터리 및 마운트된 파일 공유에서 정보를 유지하는 경우 모범 사례를 적용합니다.

## <a name="use-hello-clouddrive-command"></a>사용 하 여 hello `clouddrive` 명령
클라우드 셸을 사용 하 여 호출 하는 명령을 실행할 수 있습니다 `clouddrive`, 어떤 있습니다 toomanually 업데이트 hello 파일 공유는 탑재 된 tooCloud 셸 수 있습니다.
![Hello "clouddrive" 명령을 실행합니다.](media/clouddrive-h.png)

## <a name="mount-a-new-clouddrive"></a>새 `clouddrive` 마운트

### <a name="prerequisites-for-manual-mounting"></a>수동 마운트를 위한 필수 구성 요소
Hello를 사용 하 여 클라우드 셸와 관련 된 hello 파일 공유를 업데이트할 수 있습니다 `clouddrive mount` 명령입니다.

기존 파일 공유를 탑재 하는 경우 hello 저장소 계정은 다음과 같아야 합니다.
* 로컬 중복 저장소 또는 지역 중복 저장소 toosupport 파일을 공유합니다.
* 할당된 지역에 위치합니다. 온 보 딩을 hello 영역 할당 된 경우 hello 리소스 그룹 이름에 나열 된 toois `cloud-shell-storage-<region>`합니다.

### <a name="supported-storage-regions"></a>지원되는 저장소 지역
hello Azure 파일에에서 있어야 hello 동일 하도록 탑재 하는 hello 클라우드 셸 컴퓨터와 지역의 합니다. 클라우드 셸 클러스터는 현재 hello 다음 영역에에서 존재 합니다.
|영역|지역|
|---|---|
|아메리카|미국 동부, 미국 중남부, 미국 서부|
|유럽|북유럽, 서유럽|
|아시아 태평양|인도 중부, 동남 아시아|

### <a name="hello-clouddrive-mount-command"></a>hello `clouddrive mount` 명령

> [!NOTE]
> 새 사용자 이미지에 대해 만든 새 파일 공유를 탑재 하는 경우 프로그램 `$Home` 디렉터리 때문에 이전 `$Home` hello 이전 파일 공유에 유지 되는 이미지입니다.

Hello 실행 `clouddrive mount` 명령 hello 매개 변수 뒤에:

```
clouddrive mount -s mySubscription -g myRG -n storageAccountName -f fileShareName
```

자세한 내용은 실행 tooview `clouddrive mount -h`여기 표시 된 것 처럼:

![실행 중인 hello ' clouddrive mount'command](media/mount-h.png)

## <a name="unmount-clouddrive"></a>`clouddrive` 마운트 해제
파일 공유는 탑재 된 tooCloud 셸 언제 든 지 분리할 수 있습니다. 파일 공유를 탑재 됩니다 증명된 toomount 새 파일 공유 이전 tooyour 다음 세션.

클라우드 셸에서 tooremove 파일을 공유 합니다.
1. `clouddrive unmount`을 실행합니다.
2. 승인 하 고 hello 메시지를 확인 합니다.

파일 공유는 수동으로 삭제 하지 않는 한 tooexist를 계속 합니다. Cloud Shell은 후속 세션에서 이 파일 공유를 더 이상 검색하지 않습니다.

자세한 내용은 실행 tooview `clouddrive unmount -h`여기 표시 된 것 처럼:

![실행 중인 hello ' clouddrive unmount'command](media/unmount-h.png)

> [!WARNING]
> 이 명령을 실행하면 리소스가 삭제되지 않습니다. 셸 영구적으로 삭제 됩니다 tooCloud 매핑된 리소스 그룹, 저장소 계정 또는 파일 공유를 수동으로 삭제 하면 `$Home` 이미지 디렉터리 및 파일 공유에서 다른 파일입니다. 이 작업은 취소할 수 없습니다.

## <a name="list-clouddrive-file-shares"></a>`clouddrive` 파일 공유 나열
사용할 파일 공유로 탑재 됩니다 toodiscover `clouddrive`, hello 다음 실행 `df` 명령입니다. 

hello 파일 경로 tooclouddrive hello URL에서 공유 하는 저장소 계정 이름 및 파일을 보여 줍니다. 예를 들어 `//storageaccountname.file.core.windows.net/filesharename`

```
justin@Azure:~$ df
Filesystem                                               1K-blocks     Used Available Use% Mounted on
overlay                                                   30428648 15585636  14826628  52% /
tmpfs                                                       986704        0    986704   0% /dev
tmpfs                                                       986704        0    986704   0% /sys/fs/cgroup
/dev/sda1                                                 30428648 15585636  14826628  52% /etc/hosts
shm                                                          65536        0     65536   0% /dev/shm
//mystoragename.file.core.windows.net/fileshareName        6291456  5242944   1048512  84% /usr/justin/clouddrive
/dev/loop0                                                 5160576   601652   4296780  13% /home/justin
```

## <a name="transfer-local-files-toocloud-shell"></a>로컬 파일 tooCloud 셸 전송
hello `clouddrive` hello Azure 포털 저장소 블레이드와 디렉터리 동기화 합니다. 이 블레이드 tootransfer 로컬 파일 tooor 파일 공유에서 사용 합니다. 클라우드 셸 내에서 파일을 업데이트 hello 블레이드를 새로 고칠 때 hello 파일 저장소 GUI에에서 반영 됩니다.

### <a name="download-files"></a>파일 다운로드

![로컬 파일 목록](media/download.png)
1. Azure 포털 hello toohello 탑재 된 파일 공유를 이동 합니다.
2. Hello 대상 파일을 선택 합니다.
3. 선택 hello **다운로드** 단추입니다.

### <a name="upload-files"></a>파일 업로드

![로컬 파일 toobe 업로드](media/upload.png)
1. Tooyour 탑재 된 파일 공유를 이동 합니다.
2. 선택 hello **업로드** 단추입니다.
3. Hello 파일 또는 tooupload 원하는 파일을 선택 합니다.
4. Hello 업로드를 확인 합니다.

이제 표시 hello 파일에 액세스할 수 있는 프로그램 `clouddrive` 클라우드 셸에서 디렉터리입니다.

## <a name="next-steps"></a>다음 단계
[Cloud Shell 빠른 시작](quickstart.md) <br>
[Azure File Storage에 대해 알아보기](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage) <br>
[저장소 태그에 대해 알아보기](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) <br>
