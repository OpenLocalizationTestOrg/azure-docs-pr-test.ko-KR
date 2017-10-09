---
title: "Windows VM 배포 클래식 aaaTroubleshoot | Microsoft Docs"
description: "Azure에서 새 Windows 가상 컴퓨터를 만드는 경우 클래식 배포 문제 해결"
services: virtual-machines-windows
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 9f01d237-ba39-4c32-b72d-18f5f505d43a
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: cjiang
ms.openlocfilehash: aa12cb013a18e0572fbef8b7ea69106dd47c1fd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-creating-a-new-windows-virtual-machine-in-azure"></a>Azure에서 새 Windows 가상 컴퓨터 생성 관련 클래식 배포 문제 해결
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-selectors](../../../../includes/virtual-machines-windows-troubleshoot-deployment-new-vm-selectors-include.md)]

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

> [!IMPORTANT] 
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다. 이 문서의 hello 리소스 관리자 버전에 대 한 참조 [여기](../../virtual-machines-windows-troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a>감사 로그 수집
문제 해결, toostart 수집 hello 감사 hello 문제와 연결 된 tooidentify hello 오류를 기록 합니다.

Hello Azure 포털에서에서 클릭 **찾아보기** > **가상 컴퓨터** > *Windows 가상 컴퓨터*  >   **설정** > **감사 로그**합니다.

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-windows-troubleshoot-deployment-new-vm-table](../../../../includes/virtual-machines-windows-troubleshoot-deployment-new-vm-table.md)]

**Y:** hello 운영 체제를 일반화 하는 Windows 및 이며 업로드 또는 설정, 일반화 hello를 사용 하 여 캡처할 경우 오류 수 없습니다. 마찬가지로, hello 운영 체제는 Windows 특수화 되 고 업로드 하거나 사용 하 여 캡처할 hello 오류 않을 다음 설정을 특수화 된입니다.

**업로드 오류:**

**N<sup>1</sup>:** hello OS 일반화, Windows 이며으로 업로드 되는 경우 특수화를 얻게 됩니다 VM hello OOBE 화면에서 중단 하는 hello로 프로 비전 시간 초과 오류입니다.

**N<sup>2</sup>:** hello OS Windows 특수화 및 일반화 된 대로 업로드 이면 얻게 됩니다 hello 새 VM으로 실행 hello 원래 컴퓨터 hello OOBE 화면에서 중단 되는 VM hello로 프로 비전 실패 오류 이름, 사용자 이름 및 암호를 제공 합니다.

**해결 방법:**

tooresolve 이러한 두 오류 업로드 원본 VHD를 사용할 수 있는 온-프레미스 hello, 동일한 hello hello (일반화/특수화) 운영 체제에 대 한 유형을 설정 합니다. tooupload 일반화 하면 대로 먼저 toorun sysprep를 기억 합니다. 참조 [만들기 및 업로드 Windows Server VHD tooAzure](createupload-vhd.md) 자세한 정보에 대 한 합니다.

**캡처 오류:**

**N<sup>3</sup>:** hello OS 일반화, Windows로 캡처된 경우 특수화를 얻게 됩니다 프로비저닝 시간 초과 오류가 hello 원래 VM 사용 가능 하지 않습니다 일반화 된 상태로 표시 되기 때문에 있습니다.

**N<sup>4</sup>:** hello 새 VM으로 실행 hello 원래 컴퓨터 이름, 사용자 이름 및 암호 프로 비전 실패 오류가 hello OS Windows 특수화 및 일반화 된 대로 캡처 이면 발생 합니다. 또한 hello 원본 VM을 사용할 수 없으면 표시 되어 있으므로 같이 특수 합니다.

**해결 방법:**

tooresolve 이러한 두 오류 hello 포털에서 hello 현재 이미지를 삭제 하 고 [hello에서 다시 캡처 현재 Vhd](capture-image.md) 와 hello hello (일반화/특수화) 운영 체제에 대 한 설정 것과 동일한 합니다.

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a>문제: 사용자 지정/ 갤러리/ 마켓플레이스 이미지; 할당 오류
이 오류는 hello 새 VM 요청을 보내면 tooa 클러스터 사용 가능한 공간 tooaccommodate hello 요청을 포함 하지 않는 하는 경우에 발생 또는 요청 된 hello v M 크기를 지원할 수 없습니다. 가능한 toomix 다른 계열 없으면 hello에 있는 Vm의 동일한 클라우드 서비스입니다. 따라서 클라우드 서비스에서 지원할 수 있는 보다 다른 크기의 새 VM toocreate 원하는 hello 계산 요청이 실패 합니다.

Toocreate 사용 hello 클라우드 서비스의 hello 제약 조건에 따라 새 VM hello, 두 가지 상황 중 하나로 인해 오류가 발생할 수 있습니다.

**원인 1:** hello 클라우드 서비스는 고정 된 tooa 특정 클러스터 또는 연결 된 tooan 선호도 그룹 이며 따라서 고정된 tooa 특정 클러스터 설계 합니다. Hello hello 기존 리소스 호스팅되는 동일한 클러스터에 해당 선호도 그룹으로 새 계산 리소스를 요청 하도록 시도 됩니다. 그러나 hello 동일한 클러스터 수 없거나 지원 hello 요청 된 VM 크기 또는 할당 오류 사용 가능한 공간이 부족 한 것입니다. 마찬가지 기존 클라우드 서비스 또는 새 클라우드 서비스를 통해 hello 새 리소스가 생성 여부입니다.

**해결 방법 1:**

* 새 클라우드 서비스를 만들어서 지역 또는 지역 기반 가상 네트워크와 연결합니다.
* Hello 새 클라우드 서비스에서 새 VM을 만듭니다.
  Toocreate 새 클라우드 서비스는 동안 오류가 발생 합니다 나중에 다시 시도 하거나 다른 곳으로 hello 클라우드 서비스에 대 한 hello 영역을 변경 합니다.

> [!IMPORTANT]
> Toocreate 기존 클라우드 서비스에서 새 VM을 시도 하지만, 없습니다 및 toocreate 새 VM에 대 한 새 클라우드 서비스에 선택할 수 있습니다 tooconsolidate 모든 Vm hello에서 동일한 클라우드 서비스입니다. 따라서 toodo hello 기존 클라우드 서비스의 hello Vm을 삭제 하 고 hello 새 클라우드 서비스에서 해당 디스크에서 다시 캡처할. 그러나 것이 중요 한 tooremember hello 새 클라우드 서비스 들이 있는 새 이름 및 VIP를 tooupdate 해야 하므로 현재 hello 기존 클라우드 서비스에 대 한이 정보를 사용 하는 모든 hello 종속성에 대 한 이러한 합니다.
> 
> 

**원인 2:** hello 클라우드 서비스는 고정 된 tooa 특정 클러스터 설계 되기 때문 tooan 연결 된 선호도 그룹을 가상 네트워크와 연결 합니다. 따라서 해당 선호도 그룹의 모든 새로운 계산 리소스를 요청은 hello hello 기존 리소스 호스팅되는 동일한 클러스터에 시도 됩니다. 그러나 hello 동일한 클러스터 수 없거나 지원 hello 요청 된 VM 크기 또는 할당 오류 사용 가능한 공간이 부족 한 것입니다. 마찬가지 기존 클라우드 서비스 또는 새 클라우드 서비스를 통해 hello 새 리소스가 생성 여부입니다.

**해결 방법 2:**

* 새 지역 가상 네트워크를 만듭니다.
* 만들 hello 새 가상 네트워크에서 새 VM hello 합니다.
* [기존 가상 네트워크가 연결](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/) toohello 새 가상 네트워크입니다. [지역 가상 네트워크](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/)에 대한 자세한 내용을 참조하세요. 수 또는 [가상 네트워크를 선호도 그룹 기반 tooa 지역 가상 네트워크 마이그레이션](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/), 한 다음 만들 새 VM hello 합니다.

## <a name="next-steps"></a>다음 단계
중지된 Windows VM을 시작하거나 Azure에서 기존 Windows VM의 크기를 조정할 때 문제가 발생하면 [Azure의 기존 Windows 가상 컴퓨터 재시작 또는 크기 조정 관련 클래식 배포 문제 해결](virtual-machines-windows-classic-restart-resize-error-troubleshooting.md)을 참조하세요.

