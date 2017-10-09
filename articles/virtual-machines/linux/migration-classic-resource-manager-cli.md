---
title: "aaaMigrate Vm tooResource Azure CLI를 사용 하 여 관리자 | Microsoft Docs"
description: "이 문서에서는 안내 리소스의 플랫폼에서 지 원하는 마이그레이션 hello 클래식 tooAzure 리소스 관리자에서에서 Azure CLI를 사용 하 여"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d6f5a877-05b6-4127-a545-3f5bede4e479
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 0b11f4bb1b4658b3e88bf7629147ed953b678556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-cli"></a>Azure CLI를 사용 하 여 IaaS 리소스 클래식 tooAzure 리소스 관리자에서 마이그레이션
이러한 단계 toouse Azure CLI (명령줄 인터페이스) hello 클래식 배포 모델 toohello Azure 리소스 관리자 배포 모델에서 서비스 (IaaS) 리소스로 toomigrate 인프라에 명령 하는 방법을 보여 줍니다. hello 문서 필요 hello [Azure CLI](../../cli-install-nodejs.md)합니다.

> [!NOTE]
> 여기에서 설명 하는 모든 hello 작업은 idempotent입니다. 지원 되지 않는 기능 또는 구성 오류 이외의 문제가 있는 경우 hello를 다시 시도 하는 것이 좋습니다 준비, 중단 또는 작업을 커밋합니다. hello 플랫폼은 hello 작업을 다시 시도 합니다.
> 
> 

<br>
다음 단계는 toobe 마이그레이션 프로세스 중에 실행 해야 하는 순서도 tooidentify hello 순서는

![Hello 마이그레이션 단계를 보여 주는 스크린샷](../windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-prepare-for-migration"></a>1단계: 마이그레이션 준비
클래식 tooResource 관리자에서에서 IaaS 리소스를 마이그레이션하기를 평가할 때 권장 되는 몇 가지 모범 사례는 다음과 같습니다.

* Hello 자세히 읽고 [목록은 지원 되지 않는 구성 또는 기능이](../windows/migration-classic-resource-manager-overview.md)합니다. 지원 되지 않는 구성 또는 기능을 사용 하는 가상 컴퓨터를 설정한 경우에 발표 hello 기능/구성 지원 toobe 나올 때까지 기다리는 것이 좋습니다. 또는 해당 기능을 제거 하거나 필요에 맞도록 하는 경우 해당 구성 tooenable 마이그레이션을 외부로 이동할 수 있습니다.
* 현재 인프라 및 응용 프로그램을 배포 하는 스크립트를 자동화 하는 경우 마이그레이션에 대 한 이러한 스크립트를 사용 하 여 toocreate 유사한 테스트 설치 프로그램을 시도 하십시오. Hello Azure 포털을 사용 하 여 샘플 환경, 설정할 수 있습니다.

> [!IMPORTANT]
> 응용 프로그램 게이트웨이 클래식 tooResource 관리자에서에서 마이그레이션에 대 한 현재 지원 되지 않습니다. toomigrate 응용 프로그램 게이트웨이 사용 하 여 클래식 가상 네트워크 준비 작업 toomove hello 네트워크를 실행 하기 전에 hello 게이트웨이 제거 합니다. Hello 마이그레이션을 완료 한 후 hello Azure 리소스 관리자에서 게이트웨이 다시 연결 합니다. 
>
>Express 경로 게이트웨이 tooExpressRoute 회로 다른 구독에 연결 하는 자동으로 마이그레이션할 수 없습니다. 이러한 경우 hello express 경로 게이트웨이 제거 하 고 hello 가상 네트워크 마이그레이션 다음 hello 게이트웨이 다시 만듭니다. 참조 하십시오 [마이그레이션할 ExpressRoute 회로 및 가상 네트워크를 hello 클래식 toohello 리소스 관리자 배포 모델에서 연결 된](../../expressroute/expressroute-migration-classic-resource-manager.md) 자세한 정보에 대 한 합니다.
> 
> 

## <a name="step-2-set-your-subscription-and-register-hello-provider"></a>2 단계: 구독을 설정 하 고 hello 공급자 등록
마이그레이션 시나리오에 대 한 필요한 tooset 모두 기본에 대 한 사용자 환경 및 리소스 관리자입니다. [Azure CLI를 설치](../../cli-install-nodejs.md)하고 [구독을 선택](../../xplat-cli-connect.md)합니다.

Tooyour 로그인 계정입니다.

    azure login

다음 명령을 hello를 사용 하 여 hello Azure 구독을 선택 합니다.

    azure account set "<azure-subscription-name>"

> [!NOTE]
> 등록은 한 번 단계 보이지만 필요 toobe 마이그레이션을 시도 하기 전에 한 번 수행 합니다. 등록 하지 않고 hello 다음과 같은 오류 메시지가 표시 됩니다. 
> 
> *BadRequest : 구독이 마이그레이션에 대해 등록되지 않았습니다.* 
> 
> 

다음 명령을 hello를 사용 하 여 hello 마이그레이션 리소스 공급자를 등록 합니다. 일부 경우에 이 명령이 시간 초과됩니다. 그러나 hello 등록 성공적으로 수행 됩니다.

    azure provider register Microsoft.ClassicInfrastructureMigrate

5 분까지 hello 등록 toofinish 잠시 기다려 주십시오. 다음 명령을 hello를 사용 하 여 hello 승인의 hello 상태를 확인할 수 있습니다. 계속 진행하기 전에 RegistrationState가 `Registered` 인지 확인합니다.

    azure provider show Microsoft.ClassicInfrastructureMigrate

이제 CLI toohello 전환 `asm` 모드입니다.

    azure config mode asm

## <a name="step-3-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a>3 단계: hello VNET 또는 현재 배포의 Azure 지역에서에서 Azure 리소스 관리자 가상 컴퓨터에 충분 한 코어가 있는지 확인
이 단계에 대 한 해야 tooswitch 너무`arm` 모드입니다. 다음 명령을 hello로이 작업을 수행 합니다.

```
azure config mode arm
```

Hello 다음 CLI 명령을 toocheck hello 현재 양을 Azure 리소스 관리자에 있는 코어를 사용할 수 있습니다. 코어 할당량을 대 한 자세한 정보는 toolearn 참조 [제한 및 hello Azure 리소스 관리자](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)

```
azure vm list-usage -l "<Your VNET or Deployment's Azure region"
```

완료 하 고 나면이 단계를 확인 전환할 수 있습니다 다시 너무`asm` 모드입니다.

    azure config mode asm


## <a name="step-4-option-1---migrate-virtual-machines-in-a-cloud-service"></a>4단계: 옵션 1 - 클라우드 서비스에서 가상 컴퓨터 마이그레이션
다음 명령을, hello를 사용 하 여 클라우드 서비스로 이동한 다음 선택 hello 클라우드 서비스 toomigrate 원하는 hello 목록을 가져옵니다. Note hello 클라우드 서비스에 hello Vm 가상 네트워크에 있는 경우 또는 웹/작업자 역할이 있는 경우 오류 메시지를 받게 됩니다.

    azure service list

Hello hello 클라우드 서비스에 대 한 명령 tooget hello 배포 이름을 hello 자세한 정보를 출력에서 다음을 실행 합니다. 대부분의 경우에서 hello 배포 이름이 hello 클라우드 서비스 이름과 달라 서 hello 됩니다.

    azure service show <serviceName> -vv

첫째, 명령 뒤 hello를 사용 하 여 hello 클라우드 서비스를 마이그레이션할 수 있는 경우 유효성 검사:

```shell
azure service deployment validate-migration <serviceName> <deploymentName> new "" "" ""
```

마이그레이션에 대 한 hello 클라우드 서비스의 hello 가상 컴퓨터를 준비 합니다. 두 옵션 toochoose를 해야합니다.

Toomigrate hello Vm tooa 플랫폼 만든 가상 네트워크를 사용 하도록 하려는 경우 다음 명령을 hello를 사용 합니다.

    azure service deployment prepare-migration <serviceName> <deploymentName> new "" "" ""

Hello 리소스 관리자 배포 모델에서 가상 네트워크를 기존 toomigrate tooan 하려는 경우 다음 명령을 hello를 사용 합니다.

    azure service deployment prepare-migration <serviceName> <deploymentName> existing <destinationVNETResourceGroupName> <subnetName> <vnetName>

Hello 준비 후 작업을 완료, 전체 hello Vm의 hello 자세한 정보를 출력 tooget hello 마이그레이션 상태를 검사 하 고 hello에 포함 된 있는지 확인 하세요 `Prepared` 상태입니다.

    azure vm show <vmName> -vv

CLI 또는 hello Azure 포털을 사용 하 여 리소스를 준비 하는 hello에 대 한 hello 구성을 확인 합니다. 마이그레이션 준비 하지 않은 경우 toogo 백 toohello 이전 상태 hello 다음 명령을 사용 합니다.

    azure service deployment abort-migration <serviceName> <deploymentName>

Hello 준비 구성 좋으면, 경우에 앞으로 이동 수 있으며 hello 다음 명령을 사용 하 여 hello 리소스를 커밋할 수 있습니다.

    azure service deployment commit-migration <serviceName> <deploymentName>



## <a name="step-4-option-2----migrate-virtual-machines-in-a-virtual-network"></a>4단계: 옵션 2 - 가상 네트워크에서 가상 컴퓨터 마이그레이션
Toomigrate 않겠다고 선택 hello 가상 네트워크입니다. 지원 되지 않는 구성으로 웹/작업자 역할 또는 Vm을 포함 하는 hello 가상 네트워크를 하는 경우 얻을 수 유효성 검사 오류 메시지를 확인 합니다.

다음 명령을 hello를 사용 하 여 hello 구독에서 모든 hello 가상 네트워크를 가져옵니다.

    azure network vnet list

hello 출력에는 다음과 같이 표시 됩니다.

![Hello 전체 가상 네트워크 이름이 강조 표시 된 hello 명령줄의 스크린 샷](../media/virtual-machines-linux-cli-migration-classic-resource-manager/vnet.png)

위 예제는 hello에서 hello **virtualNetworkName** 전체 이름인 hello **"그룹 classicubuntu16 classicubuntu16"**합니다.

먼저, 다음 명령을 hello를 사용 하 여 hello 가상 네트워크를 마이그레이션할 수 있는 경우 유효성 검사:

```shell
azure network vnet validate-migration <virtualNetworkName>
```

다음 명령을 hello를 사용 하 여 마이그레이션에 대 한 hello 선택한 가상 네트워크를 준비 합니다.

    azure network vnet prepare-migration <virtualNetworkName>

CLI 또는 hello Azure 포털을 사용 하 여 가상 컴퓨터를 준비 하는 hello에 대 한 hello 구성을 확인 합니다. 마이그레이션 준비 하지 않은 경우 toogo 백 toohello 이전 상태 hello 다음 명령을 사용 합니다.

    azure network vnet abort-migration <virtualNetworkName>

Hello 준비 구성 좋으면, 경우에 앞으로 이동 수 있으며 hello 다음 명령을 사용 하 여 hello 리소스를 커밋할 수 있습니다.

    azure network vnet commit-migration <virtualNetworkName>

## <a name="step-5-migrate-a-storage-account"></a>5단계: 저장소 계정 마이그레이션
Hello 가상 컴퓨터를 마이그레이션하거나 완료 하 고 나면 hello 저장소 계정을 마이그레이션하는 것이 좋습니다.

다음 명령을 hello를 사용 하 여 마이그레이션을 위해 hello 저장소 계정 준비

    azure storage account prepare-migration <storageAccountName>

CLI 또는 hello Azure 포털을 사용 하 여 저장소 계정을 준비 하는 hello에 대 한 hello 구성을 확인 합니다. 마이그레이션 준비 하지 않은 경우 toogo 백 toohello 이전 상태 hello 다음 명령을 사용 합니다.

    azure storage account abort-migration <storageAccountName>

Hello 준비 구성 좋으면, 경우에 앞으로 이동 수 있으며 hello 다음 명령을 사용 하 여 hello 리소스를 커밋할 수 있습니다.

    azure storage account commit-migration <storageAccountName>

## <a name="next-steps"></a>다음 단계

* [클래식 tooAzure 리소스 관리자에서에서 리소스를 IaaS 플랫폼에서 지 원하는 마이그레이션 개요](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [클래식 tooAzure 리소스 관리자에서에서 마이그레이션 플랫폼 지원에 기술 심층 분석](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [클래식 tooAzure 리소스 관리자에서에서 IaaS 리소스의 마이그레이션 계획](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [클래식 tooAzure 리소스 관리자에서에서 PowerShell toomigrate IaaS 리소스를 사용 하 여](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [클래식 tooAzure 리소스 관리자에서에서 IaaS 리소스의 마이그레이션 지원에 대 한 커뮤니티 도구](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [가장 일반적인 마이그레이션 오류 검토](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [클래식 tooAzure 리소스 관리자에서에서 마이그레이션 IaaS 리소스에 대 한 가장 자주 묻는 질문 검토 hello](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
