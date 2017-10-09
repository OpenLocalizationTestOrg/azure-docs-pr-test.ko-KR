---
title: "Linux VM의 이미지 aaaCapture | Microsoft Docs"
description: "Toocapture Linux 기반 Azure 가상 컴퓨터 (VM)의 이미지 만드는 방법을 hello 클래식 배포 모델에 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17d7ffee-a58e-4290-9de1-64c3cf1ddc05
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 33c4059d5bb919a86bdc3492abca540750f365ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocapture-a-classic-linux-virtual-machine-as-an-image"></a>어떻게 toocapture 이미지 형식으로 클래식 Linux 가상 컴퓨터
> [!IMPORTANT]
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다. 너무 방법에 대해 알아봅니다[hello 리소스 관리자 모델을 사용 하 여 이러한 단계를 수행](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

이 문서에서는 어떻게 toocapture는 클래식 Azure 가상 컴퓨터 (VM) 다른 가상 컴퓨터 이미지 toocreate로 Linux를 실행 합니다. 이 이미지에 hello OS 디스크는 및 연결 된 toohello VM 데이터 디스크가 있습니다. 네트워킹 구성 tooconfigure 있으므로 포함 되지 않습니다는 만들 때 hello 다른 VM hello 이미지에서 합니다.

Azure 저장소에서 이미지 hello **이미지**, 업로드 한 모든 이미지와 함께 합니다. 이미지에 대한 자세한 내용은 [Azure의 가상 컴퓨터 이미지 정보][About Virtual Machine Images in Azure]를 참조하세요.

## <a name="before-you-begin"></a>시작하기 전에
이 단계에서는 Azure VM hello 클래식 배포 모델 및 데이터 디스크를 연결까지 포함 하는 구성 된 hello 운영 체제를 사용 하 여 이미 만든 가정 합니다. VM toocreate 해야 할 경우 읽기 [어떻게 tooCreate Linux 가상 컴퓨터를][How tooCreate a Linux Virtual Machine]합니다.

## <a name="capture-hello-virtual-machine"></a>Hello 가상 컴퓨터 캡처
1. [Toohello VM 연결](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 원하는 SSH 클라이언트를 사용 하 여 합니다.
2. Hello SSH 창의 hello 다음 명령을 입력 합니다. hello에서 출력 `waagent` hello이이 유틸리티의 버전에 따라 약간 다를 수 있습니다.

    ```bash
    sudo waagent -deprovision+user
    ```

    hello 이전 명령이 tooclean hello 시스템 고 다시 프로 비전에 맞게 사용할 수 있습니다. 이 작업 hello 다음 작업을 수행 합니다.

   * (Provisioning.RegenerateSshHostKeyPair 'y' hello 구성 파일의 경우) SSH 호스트 키를 제거 합니다.
   * /etc/resolv.conf의 Nameserver 구성을 지웁니다.
   * 제거 hello  `root` /등/그림자 (Provisioning.DeleteRootPassword hello 구성 파일에서 'y'는) 하는 경우 사용자 암호
   * 캐시된 DHCP 클라이언트 임대 제거
   * 다시 설정 합니다. 호스트 이름 toolocalhost.localdomain
   * Hello (/var/lib/waagent에서 가져온)는 마지막 프로 비전 된 사용자 계정을 삭제 **와 관련 데이터**합니다.

     > [!NOTE]
     > 데이터 너무 "일반화" hello 이미지 및 파일 삭제 프로 비전 해제 합니다. 만 VM에서 새 이미지 템플릿으로 toocapture를 만들려는 경우이 명령을 실행 합니다. Hello 이미지가 중요 한 정보를 모두 선택 취소 되어 또는 재배포 toothird 파티에 대 한 적합 한 보장 하지 않습니다.

3. 형식 **y** toocontinue 합니다. Hello를 추가할 수 있습니다 `-force` 매개 변수 tooavoid이 확인 단계입니다.
4. 형식 **종료** tooclose hello SSH 클라이언트입니다.

   > [!NOTE]
   > hello 나머지 단계 있다고 가정 이미 [hello Azure CLI 설치](../../../cli-install-nodejs.md) 클라이언트 컴퓨터에 있습니다. 단계를 수행 하는 모든 hello hello에서 수행할 수 있습니다 [Azure 포털](http://portal.azure.com)합니다.

5. 클라이언트 컴퓨터에서 Azure CLI 및 로그인 tooyour Azure 구독을 엽니다. 자세한 내용은 읽기 [hello Azure CLI에서에서 tooan Azure 구독 연결](../../../xplat-cli-connect.md)합니다.

   > [!NOTE]
   > Hello Azure 포털에서에서 toohello 포털에 로그인 합니다.

6. 서비스 관리 모드에 있는지 확인합니다.

    ```azurecli
    azure config mode asm
    ```

7. Hello 이미 프로 비전 해제 하는 VM 종료 합니다. hello 다음 예에서는 종료 hello 라는 VM `myVM`:

    ```azurecli
    azure vm shutdown myVM
    ```
   필요한 경우 모든 hello Vm이 구독에서 사용 하 여 만든 목록을 볼 수 있습니다.`azure vm list`

   > [!NOTE]
   > Hello Azure 포털을 사용 하는 경우 hello VM을 선택 하 고 클릭 **중지** hello VM 종료 합니다.

8. Hello VM이 중지 되 면 hello 이미지를 캡처하십시오. 다음 예에서는 캡처 hello hello 라는 VM `myVM` 라는 일반화 된 이미지를 만들고 `myNewVM`:

    ```azurecli
    azure vm capture -t myVM myNewVM
    ```

    hello `-t` 삭제 hello 원래 가상 컴퓨터 하위 명령입니다.

    > [!NOTE]
    > Hello Azure 포털에서에서 선택 하 여 이미지를 캡처할 수 **이미지** hello 허브 메뉴에서 합니다. 다음 hello 이미지에 대 한 정보는 toosupply hello 필요: 이름, 리소스 그룹, 위치, 운영 체제 유형 및 저장소 blob 경로입니다.

9. hello 새 이미지 될 수 있는 이미지의 hello 목록에서 사용할 수 있는 사용 된 tooconfigure 모든 새 VM입니다. Hello 명령을 사용 하 여 볼 수 있습니다.

   ```azurecli
   azure vm image list
   ```

   Hello에 [Azure 포털](http://portal.azure.com), hello에 hello 새 이미지가 나타납니다 **VM 이미지 (클래식)** toohello 속하는 **계산** 서비스입니다. 에 액세스할 수 있습니다 **VM 이미지 (클래식)** 클릭 하 여 _더 많은 서비스_ hello Azure의 hello 맨 아래에 서비스 목록 및 hello를 검색 한 다음 **계산** 서비스입니다.   

   ![이미지 캡처 성공](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a>다음 단계
hello 이미지는 사용 되는 준비 toobe toocreate Vm입니다. Hello Azure CLI 명령을 사용 하 여 `azure vm create` 및 만든 공급 hello 이미지 이름. 자세한 내용은 참조 [클래식 배포 모델에 사용 하 여 hello Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)합니다.

또는 hello를 사용 하 여 [Azure 포털](http://portal.azure.com) toocreate hello를 사용 하 여 사용자 지정 VM **이미지** 메서드 및 hello를 선택 하는 사용자가 만든 이미지입니다. 자세한 내용은 참조 [방법을 사용자 지정 VM tooCreate][How tooCreate a Custom Virtual Machine]합니다.

**참고 항목:** [Azure Linux 에이전트 사용자 가이드](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[About Virtual Machine Images in Azure]:../../virtual-machines-linux-classic-about-images.md
[How tooCreate a Custom Virtual Machine]:create-custom.md
[How tooAttach a Data Disk tooa Virtual Machine]:attach-disk.md
[How tooCreate a Linux Virtual Machine]:create-custom.md
