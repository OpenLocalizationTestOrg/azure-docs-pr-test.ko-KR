---
title: "Azure Active Directory Domain Services: 관리 가이드 | Microsoft 문서"
description: "도메인에 가입 Windows 가상 컴퓨터 tooa 관리 되는 Azure PowerShell와 hello 클래식 배포 모델을 사용 합니다."
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9143b843-7327-43c3-baab-6e24a18db25e
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 21bc5930d84c5368a120f9d81f09320e2a0168fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-windows-server-virtual-machine-tooa-managed-domain-using-powershell"></a>도메인에 가입 된 Windows Server 가상 컴퓨터 tooa 관리 되는 PowerShell을 사용 하 여
> [!div class="op_single_selector"]
> * [Azure 클래식 포털 - Windows](active-directory-ds-admin-guide-join-windows-vm.md)
> * [PowerShell - Windows](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

> [!IMPORTANT]
> Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. Azure AD 도메인 서비스는 hello 리소스 관리자 모델을 현재 지원 하지 않습니다.
>
>

이러한 단계에 만들고 빌딩 블록 방법을 사용 하 여 Windows 기반 Azure 가상 컴퓨터를 미리 구성 하는 toocustomize 집합의 Azure PowerShell 명령 하는 방법을 보여 줍니다. 다음이 단계를 사용 하 여 Windows 기반 Azure 가상 컴퓨터를 빌드하고 tooan Azure AD 도메인 서비스에 대 한 관리 되는 도메인 조인 수 수 있습니다.

다음 단계에서는 빈 칸 채우기 접근 방식에 따라 Azure PowerShell 명령 집합을 만듭니다. 이 방법은 새 tooPowerShell 또는 구성이 성공적으로 완료에 대 한 tooknow 어떤 값 toospecify 하려는 경우 유용할 수 있습니다. 고급 PowerShell 사용자 수 hello 명령을 수행 하 고 hello 변수 ("$"로 시작 하 고 hello 선)에 대 한 고유한 값을 대체 합니다.

아직 수행 하지 않은 경우의 지침에 hello를 사용 하 여 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) 로컬 컴퓨터에 Azure PowerShell tooinstall 합니다. 그런 다음 Windows PowerShell 명령 프롬프트를 엽니다.

## <a name="step-1-add-your-account"></a>1단계: 사용자 계정 추가
1. Hello PowerShell 프롬프트에서 입력 **Add-azureaccount** 클릭 **Enter**합니다.
2. Azure 구독에 연결 된 hello 전자 메일 주소에 입력 하 고 클릭 **계속**합니다.
3. Hello 계정의 암호를 입력 합니다.
4. **로그인**을 클릭합니다.

## <a name="step-2-set-your-subscription-and-storage-account"></a>2단계: 구독 및 저장소 계정 설정
Hello Windows PowerShell 명령 프롬프트에서 다음이 명령을 실행 하 여 Azure 구독 및 저장소 계정을 설정 합니다. Hello < 및 > 문자를 포함 하는 hello 따옴표 안의 hello 올바른 이름으로 대체 합니다.

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

Hello 올바른 구독 이름을 hello hello의 hello 출력의 SubscriptionName 속성에서에서 가져올 수 있습니다 **Get-azuresubscription** 명령입니다. Hello hello의 hello 출력의 Label 속성에서에서 hello 올바른 저장소 계정 이름을 가져올 수 있습니다 **Get AzureStorageAccount** hello를 실행 한 후 명령을 **Select-azuresubscription** 명령입니다.

## <a name="step-3-step-by-step-walkthrough---provision-hello-virtual-machine-and-join-it-toohello-managed-domain"></a>3 단계: 단계별 연습-hello 가상 컴퓨터를 프로 비전 하 고 toohello 관리 되는 도메인에 가입
다음 hello 해당 Azure PowerShell 명령 집합 toocreate 가독성을 위해 각 블록 사이 빈 줄이 가상 컴퓨터를은입니다.

Hello Windows 가상 컴퓨터 toobe 프로 비전에 대 한 정보를 지정 합니다.

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

D, DS 또는 G 시리즈 가상 컴퓨터에 대 한 hello InstanceSize 값, 참조 [가상 컴퓨터와 Azure 클라우드 서비스 크기](https://msdn.microsoft.com/library/azure/dn197896.aspx)합니다.

Hello 관리 되는 도메인에 대 한 정보를 제공 합니다.

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

Hello hello 클라우드 서비스 이름을 지정 합니다.

    $svcname="Contoso100-test"

VM을 가입 해야 하는 hello 가상 네트워크 toowhich hello hello 이름을 지정 합니다. 해당 hello AAD DS 관리 되는 도메인을이 가상 네트워크에서 사용할 수 있는지 확인 합니다.

    $vnetname="MyPreviewVnet"

Hello VM 이미지 사용 toobe tooprovision hello VM 선택 합니다.

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

VM-집합 VM 이름 hello 구성 인스턴스 크기 / 이미지 toobe 사용 합니다.

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

Hello VM에 대 한 로컬 관리자 자격 증명을 가져옵니다. 강력한 로컬 관리자 암호를 선택합니다.

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

Too'AAD DC 관리자 그룹 toojoin VM toohello 관리 되는 도메인에 속한 사용자 계정에 대 한 자격 증명을 얻습니다. 지정 하지 마십시오 hello 도메인 이름-인스턴스 예에서 지정 'bob'에 대 한 hello 사용자 이름으로.

    $domainadmincred=Get-Credential –Message "Now type hello name (DO NOT INCLUDE hello DOMAIN) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

도메인 가입 요구 사항 및 필요한 자격 증명 지정-hello VM을 구성 합니다.

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

Hello VM에 대 한 서브넷을 설정 합니다.

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

선택 사항: hello 도메인의 toohello IP 주소를 가리킵니다. Hello 가상 네트워크에 대 한 DNS 서버 hello Azure AD 도메인 서비스 관리 되는 도메인 toobe hello의 hello IP 주소를 설정 하면이 단계가 필요 하지 않습니다.

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

이제, 프로 비전 hello 도메인에 가입 된 Windows VM입니다.

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="script-tooprovision-a-windows-vm-and-automatically-join-it-tooan-aad-domain-services-managed-domain"></a>Windows VM tooprovision 스크립트를 자동으로 tooan AAD 도메인 서비스에 대 한 관리 되는 도메인 조인
이 PowerShell 명령 집합은 다음과 같은 LOB(기간 업무) 서버용 가상 컴퓨터를 만듭니다.

* Windows Server 2012 R2 Datacenter 이미지 hello를 사용합니다.
* 매우 작은 가상 컴퓨터임
* 이름이 hello Contoso100 테스트 합니다.
* 도메인에 가입된 toohello contoso100 관리 되는 도메인을 자동으로 됩니다.
* Toohello 추가 hello와 동일한 가상 네트워크 도메인을 관리 합니다.

다음은 hello 전체 샘플 스크립트 toocreate hello Windows 가상 컴퓨터와 자동으로 toohello Azure AD 도메인 서비스에 대 한 관리 되는 도메인 조인 합니다.

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

    $svcname="Contoso100-test"
    $vnetname="MyPreviewVnet"

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

    $domainadmincred=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="related-content"></a>관련 콘텐츠
* [Azure AD Domain Services - 시작 가이드](active-directory-ds-getting-started.md)
* [Azure AD 도메인 서비스 관리되는 도메인 관리](active-directory-ds-admin-guide-administer-domain.md)
