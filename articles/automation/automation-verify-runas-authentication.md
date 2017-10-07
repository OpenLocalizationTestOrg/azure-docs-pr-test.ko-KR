---
title: "aaaValidate Azure 자동화 계정 구성 | Microsoft Docs"
description: "이 문서는 어떻게 자동화 계정의 tooconfirm hello 구성이 제대로 설치를 설명 합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: magoedte
ms.openlocfilehash: 3a990dcc6661cf67c4b62592ce03d55a3791053a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="test-azure-automation-run-as-account-authentication"></a>Azure Automation 실행 계정 인증 테스트
자동화 계정을 성공적으로 만들어지면 후 수 있는 간단한 테스트 tooconfirm을 수행할 수 있습니다 toosuccessfully 인증할 Azure 리소스 관리자 또는 Azure 클래식 배포 계정을 사용 하 여 새로 만들거나 업데이트 자동화 계정으로 실행 합니다.    

## <a name="automation-run-as-authentication"></a>Automation 실행 인증
Hello 다음 예제 코드를 사용 하 여 너무[PowerShell runbook을 만들](automation-creating-importing-runbook.md) hello를 사용 하 여 tooverify 인증 계정으로 뿐 아니라 사용자 지정 runbook tooauthenticate에 실행 하 고 자동화 계정 사용 하 여 리소스 관리자 리소스를 관리 합니다.   

    $connectionName = "AzureRunAsConnection"
    try
    {
        # Get hello connection "AzureRunAsConnection "
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

        "Logging in tooAzure..."
        Add-AzureRmAccount `
           -ServicePrincipal `
           -TenantId $servicePrincipalConnection.TenantId `
           -ApplicationId $servicePrincipalConnection.ApplicationId `
           -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
    }
    catch {
       if (!$servicePrincipalConnection)
       {
          $ErrorMessage = "Connection $connectionName not found."
          throw $ErrorMessage
      } else{
          Write-Error -Message $_.Exception
          throw $_.Exception
      }
    }

    #Get all ARM resources from all resource groups
    $ResourceGroups = Get-AzureRmResourceGroup 

    foreach ($ResourceGroup in $ResourceGroups)
    {    
       Write-Output ("Showing resources in resource group " + $ResourceGroup.ResourceGroupName)
       $Resources = Find-AzureRmResource -ResourceGroupNameContains $ResourceGroup.ResourceGroupName | Select ResourceName, ResourceType
       ForEach ($Resource in $Resources)
       {
          Write-Output ($Resource.ResourceName + " of type " +  $Resource.ResourceType)
       }
       Write-Output ("")
    } 

인증에 사용 되는 cmdlet hello 확인 hello runbook-에서 **추가 AzureRmAccount**, 사용 하 여 hello *ServicePrincipalCertificate* 매개 변수 집합입니다.  이것은 자격 증명이 아니라 서비스 주체 인증서를 사용하여 인증합니다.  

때 있습니다 [hello runbook을 실행](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate 계정으로 실행 계정에는 [runbook 작업](automation-runbook-execution.md) 가 만들어지면 hello 작업 블레이드에서 표시 되 고 hello에 hello 작업 상태 표시 **작업 요약**바둑판식으로 배열 합니다. 작업 상태 hello로 시작 됩니다 *큐 대기* hello 클라우드 toobecome 사용할 수 있는에 runbook worker를 대기 하 고 있음을 나타내는입니다. 도 이동 후 됩니다*시작* 작업자 hello 작업 요구 한 경우 다음 *실행* hello runbook 실제로 실행을 시작한 경우.  상태를 확인할 hello runbook 작업이 완료 되 면 **Completed**합니다.

toosee hello runbook의 자세한 결과 hello hello를 클릭 하십시오. **출력** 바둑판식으로 배열입니다.  Hello에 **출력** 블레이드를 표시 되어야가 성공적으로 인증 하 고 구독에서 모든 리소스 그룹의 모든 리소스의 목록을 반환 합니다.  

Tooremove hello hello 주석으로 시작 하는 코드 블록 기억 `#Get all ARM resources from all resource groups` runbook에 대 한 hello 코드를 재사용 있습니다.

## <a name="classic-run-as-authentication"></a>클래식 실행 인증
너무 hello 다음 예제 코드를 사용 하 여[PowerShell runbook을 만들](automation-creating-importing-runbook.md) 클래식 hello 사용 하 여 tooverify 인증 계정 및 사용자 지정 runbook tooauthenticate에서를 실행 하 고 hello 클래식 배포 모델에는 리소스를 관리 합니다.  

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID
    
    #Get all VMs in hello subscription and return list with name of each
    Get-AzureVM | ft Name

때 있습니다 [hello runbook을 실행](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate 계정으로 실행 계정에는 [runbook 작업](automation-runbook-execution.md) 가 만들어지면 hello 작업 블레이드에서 표시 되 고 hello에 hello 작업 상태 표시 **작업 요약**바둑판식으로 배열 합니다. 작업 상태 hello로 시작 됩니다 *큐 대기* hello 클라우드 toobecome 사용할 수 있는에 runbook worker를 대기 하 고 있음을 나타내는입니다. 도 이동 후 됩니다*시작* 작업자 hello 작업 요구 한 경우 다음 *실행* hello runbook 실제로 실행을 시작한 경우.  상태를 확인할 hello runbook 작업이 완료 되 면 **Completed**합니다.

toosee hello runbook의 자세한 결과 hello hello를 클릭 하십시오. **출력** 바둑판식으로 배열입니다.  Hello에 **출력** 블레이드를 표시 되어야가 성공적으로 인증 하 고 구독에 배포 되는 VMName 하 여 모든 Azure Vm의 목록을 반환 합니다.  

Tooremove hello cmdlet 기억 **Get-azurevm** runbook에 대 한 hello 코드를 재사용 있습니다.

## <a name="next-steps"></a>다음 단계
* PowerShell runbook 시작 tooget 참조 [내 첫 번째 PowerShell runbook](automation-first-runbook-textual-powershell.md)합니다.
* 그래픽 작성에 대 한 더 toolearn 참조 [Azure 자동화의 그래픽 제작](automation-graphical-authoring-intro.md)합니다.
