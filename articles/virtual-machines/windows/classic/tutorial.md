---
title: "hello Azure 포털에서에서 VM aaaCreate | Microsoft Docs"
description: "Hello Azure 포털에서에서 Windows 가상 컴퓨터를 만듭니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1871f823-ebd7-4eff-9a22-8e2411555595
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 3848a3d06a7ce377633db78ea385826ed40f94fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-running-windows-in-hello-azure-portal"></a>Hello Azure 포털에서에서 Windows를 실행 하는 가상 컴퓨터 만들기
> [!div class="op_single_selector"]
> * [Azure 포털](tutorial.md)
> * [PowerShell: 클래식 배포](create-powershell.md)
>
>

<br>

> [!IMPORTANT]
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다. 너무 방법에 대해 알아봅니다[hello 리소스 관리자 배포 모델을 사용 하 여 이러한 단계를 수행](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) hello를 사용 하 여 **Azure 포털**합니다.

이 자습서에서는 어떻게 toocreate Azure 가상 컴퓨터 (VM) hello Azure 포털에서에서 Windows를 실행 합니다. 예를 들어, Windows Server 이미지에서는 하지만 하는 것 외의 hello 여러 Azure 제안의 이미지입니다. 참고: 이미지 선택은 구독에 따라 달라집니다. 예를 들어 Windows 데스크톱 이미지는 사용 가능한 tooMSDN 구독자 수 있습니다.

이 섹션에서는 toouse hello **대시보드** Azure 포털 tooselect hello와 다음 hello 가상 컴퓨터를 만듭니다.

[사용자 고유의 이미지](createupload-vhd.md)를 사용하여 VM을 만들 수도 있습니다. toolearn이 및 다른 방법에 대 한 참조 [Windows 가상 컴퓨터를 다른 방법으로 toocreate](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

<!-- 02/27/2017 Video removed as it was based on hello classic portal. -->

## <a id="createvirtualmachine"></a>Hello 가상 컴퓨터 만들기
[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[hello 리소스 관리자 배포 모델을 사용 하 여 VM 만들기](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) hello Azure 포털의에서.
* Toohello 가상 컴퓨터에 로그온 합니다. 자세한 내용은 [Windows Server를 실행 하는 tooa 가상 컴퓨터에 로그온](connect-logon.md)합니다.
* 디스크 toostore 데이터에 연결 합니다. 빈 디스크와 데이터가 포함된 디스크를 모두 연결할 수 있습니다. 자세한 내용은 hello [hello 클래식 배포 모델을 사용 하 여 만든 데이터 디스크 tooa Windows 가상 컴퓨터를 연결](attach-disk.md)합니다.
