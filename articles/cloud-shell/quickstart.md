---
title: "aaaAzure 클라우드 셸 (미리 보기) 빠른 시작 | Microsoft Docs"
description: "Azure 클라우드 셸 hello에 대 한 빠른 시작"
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
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: e60700b92c10c331910dd8bb3c627fe1a024091c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-for-using-hello-azure-cloud-shell"></a>Azure 클라우드 셸 hello를 사용 하 여에 대 한 빠른 시작

이 문서에 toouse Azure 클라우드 셸 hello에 hello 하는 방법을 자세히 설명 [Azure 포털](https://ms.portal.azure.com/)합니다.

## <a name="start-cloud-shell"></a>Cloud Shell 시작
1. 시작 **클라우드 셸** hello Azure 포털의 위쪽 탐색 hello에서 <br>
![](media/shell-icon.png)
2. 구독 toocreate 저장소 계정 및 Azure 파일 공유 선택
3. "저장소 만들기"를 선택합니다.

> [!TIP]
> 모든 세션에서 Azure CLI 2.0에 대해 자동으로 인증됩니다.

### <a name="set-your-subscription"></a>구독을 설정합니다.
1. 액세스할 수 있는 구독을 나열합니다. <br>
`az account list`
2. 기본 구독을 설정합니다. <br>
`az account set --subscription my-subscription-name`

> [!TIP]
> `/home/<user>/.azure/azureProfile.json`을 사용하여 이후 세션에서 구독을 기억합니다.

### <a name="create-a-resource-group"></a>리소스 그룹 만들기
미국 서부에 “MyRG”라는 새 리소스 그룹을 만듭니다. <br>
`az group create -l westus -n MyRG` <br>

### <a name="create-a-linux-vm"></a>Linux VM 만들기
새 리소스 그룹에서 Ubuntu VM을 만듭니다. 이러한 SSH 키 및 설치 hello VM hello Azure CLI 2.0 만들어집니다. <br>
`az vm create -n my_vm_name -g MyRG --image UbuntuLTS --generate-ssh-keys`

> [!NOTE]
> VM에 배치 되는 사용 되는 공용 및 개인 키 tooauthenticate hello `/User/.ssh/id_rsa` 및 `/User/.ssh/id_rsa.pub` 기본적으로 Azure CLI 2.0. .ssh 폴더는 연결된 Azure 파일 공유의 5GB 이미지에서 유지됩니다.

이 VM의 사용자 이름은 Cloud Shell에서 사용되는 사용자 이름입니다($User@Azure:).

### <a name="ssh-into-your-linux-vm"></a>Linux VM으로 SSH
1. Hello Azure 포털 검색 표시줄에서 VM 이름을 검색 합니다.
2. "연결"을 클릭하고 다음을 실행합니다.`ssh username@ipaddress`

![](media/sshcmd-copy.png)

Hello SSH 연결을 설정할 때 Ubuntu 시작 프롬프트 hello 표시 되어야 합니다.
![](media/ubuntu-welcome.png)

## <a name="cleaning-up"></a>정리 
리소스 그룹 및 해당 그룹 내의 모든 리소스를 삭제합니다. <br>
`az group delete -n MyRG`을 실행합니다.

## <a name="next-steps"></a>다음 단계
[Cloud Shell의 저장소 유지 알아보기](persisting-shell-storage.md) <br>
[Azure CLI 2.0에 대해 알아보기](https://docs.microsoft.com/cli/azure/) <br>
[Azure File Storage에 대해 알아보기](../storage/files/storage-files-introduction.md) <br>