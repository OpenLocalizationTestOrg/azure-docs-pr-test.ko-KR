---
title: "aaaConnect PowerShell을 사용 하 여 응용 프로그램 tooyour 가상 네트워크"
description: "PowerShell을 사용 하 여 tooconnect tooand 가상 네트워크와 작동 하는 방법에 대 한 지침"
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: cephalin
ms.assetid: a5c76e77-972a-431c-b14b-3611dae1631b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/29/2016
ms.author: ccompy
ms.openlocfilehash: c9d0fa99d02cab7b2c7211a1b2f7b7d0cd27ee8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-app-tooyour-virtual-network-by-using-powershell"></a>PowerShell을 사용 하 여 응용 프로그램 tooyour 가상 네트워크 연결
## <a name="overview"></a>개요
Azure 앱 서비스의 응용 프로그램 (웹, 모바일, 또는 API)를 연결할 수 있습니다 tooan 구독에서 Azure 가상 네트워크 (VNet). 이 기능은 VNet 통합이라고 합니다. hello VNet 통합 기능 toorun 가상 네트워크에 Azure 앱 서비스의 인스턴스 수 있는 hello 앱 서비스 환경 기능을 사용 하면 일치 하지 않습니다.

hello VNet 통합 기능에 toointegrate hello 클래식 배포 모델 또는 hello Azure 리소스 관리자 배포 모델을 사용 하 여 배포 되는 가상 네트워크에 사용할 수 있는 hello 새로운 포털에서 사용자 인터페이스 (UI) 있습니다. Toolearn hello 기능에 대 한 자세한 참조 [앱을 Azure 가상 네트워크와 통합](web-sites-integrate-with-vnet.md)합니다.

이 문서는 toouse UI hello 하는 방법에 대 한 하지 않지만 대신 방법에 대 한 PowerShell을 사용 하 여 tooenable 통합 합니다. 각 배포 모델에 대 한 hello 명령에서 다른 되므로이 문서는 각 배포 모델에 대 한 섹션을 있습니다.  

이 문서를 진행하기 전에 다음이 있는지 확인합니다.

* 최신 Azure PowerShell SDK를 설치 하는 번호입니다. 웹 플랫폼 설치 관리자 hello로이 설치할 수 있습니다.
* 표준 또는 프리미엄 SKU에서 실행 중인 Azure 앱 서비스의 앱

## <a name="classic-virtual-networks"></a>클래식 가상 네트워크
이 섹션에서는 hello 클래식 배포 모델을 사용 하는 가상 네트워크에 대 한 세 가지 작업을 설명 합니다.

1. 응용 프로그램 tooa 기존 가상 네트워크 게이트웨이 않았으며 지점 및 사이트 연결에 대해 구성 되어 있는 연결 합니다.
2. 앱에 대한 가상 네트워크 통합 정보를 업데이트합니다.
3. 가상 네트워크에서 앱 연결을 끊습니다.

### <a name="connect-an-app-tooa-classic-vnet"></a>응용 프로그램 tooa 연결 클래식 VNet
tooconnect 앱 tooa 가상 네트워크는 다음 세 가지 단계를 따르십시오.

1. 것은 될 특정 가상 네트워크에 연결할 toohello 웹 앱을 선언 합니다. hello 앱 지점 및 사이트 간 연결용 가상 네트워크 toohello 제공 될 인증서를 생성 합니다.
2. Hello 웹 응용 프로그램 인증서 toohello 가상 네트워크를 업로드 하 고 hello 지점-사이트 VPN 패키지 URI를 검색 합니다.
3. Hello 지점 및 사이트 패키지 URI와 hello 웹 응용 프로그램의 가상 네트워크 연결을 업데이트 합니다.

hello 첫 번째 및 세 번째 단계는 완전히 스크립트 가능 하지만 두 번째 단계 hello hello 포털 또는 액세스 tooperform을 통해 일회성 인 수동 작업이 필요한 **배치** 또는 **패치** hello 가상 네트워크에 대 한 작업 Azure 리소스 관리자 끝점입니다. 이 옵션을 사용 toohave Azure 지원에 문의 합니다. 시작하기 전에 게이트웨이가 설정되고 배포된 지점 및 사이트 간 연결이 이미 활성화된 클래식 가상 네트워크가 있는지 확인합니다. toocreate hello 게이트웨이 사용 하도록 설정한 지점 및 사이트 간 연결, 필요한 toouse hello 포털에 설명 된 대로 [VPN 게이트웨이 만들지][createvpngateway]합니다.

hello 클래식 가상 네트워크 필요 toobe hello에 앱 서비스와 같은 구독을 통합 하는 해당 보류 hello 응용 프로그램을 계획 합니다.

##### <a name="set-up-azure-powershell-sdk"></a>Azure PowerShell SDK 설정
PowerShell 창을 열고 다음을 사용하여 Azure 계정 및 구독을 설정합니다.

    Login-AzureRmAccount

해당 명령의 열립니다 Azure 자격 증명 프롬프트 tooget 됩니다. 에 로그인 한 후 hello 명령을 tooselect hello 구독 toouse 되도록 다음 중 하나를 사용 합니다. 가상 네트워크 및 앱 서비스 계획에 있는 hello 구독을 사용 하 고 있는지 확인 합니다.

    Select-AzureRmSubscription –SubscriptionName [WebAppSubscriptionName]

또는

    Select-AzureRmSubscription –SubscriptionId [WebAppSubscriptionId]

##### <a name="variables-used-in-this-article"></a>이 문서에 사용된 변수
toosimplify 명령을 설정 해 드립니다는 **$Configuration** hello 특정 구성 사용 하 여 PowerShell 변수입니다.

매개 변수 뒤 hello로 PowerShell에서 다음과 같이 변수를 설정 합니다.

    $Configuration = @{}
    $Configuration.WebAppResourceGroup = "[Your web app resource group]"
    $Configuration.WebAppName = "[Your web app name]"
    $Configuration.VnetSubscriptionId = "[Your vnet subscription id]"
    $Configuration.VnetResourceGroup = "[Your vnet resource group]"
    $Configuration.VnetName = "[Your vnet name]"

hello 응용 프로그램 위치에는 공백 없이 hello 위치 여야 합니다. 예를 들어 미국 서부는 westus입니다.

    $Configuration.WebAppLocation = "[Your web app Location]"

hello 다음 항목은 hello 인증서 써야 합니다. 로컬 컴퓨터에서 쓰기 가능한 경로여야 합니다. Hello 끝 tooinclude.cer 있는지 확인 하십시오.

    $Configuration.GeneratedCertificatePath = "[C:\Path\To\Certificate.cer]"

toosee 설정, 형식 **$Configuration**합니다.

    > $Configuration

    Name                           Value
    ----                           -----
    GeneratedCertificatePath       C:\vnetcert.cer
    VnetSubscriptionId             efc239a4-88f9-2c5e-a9a1-3034c21ad496
    WebAppResourceGroup            vnetdemo-rg
    VnetResourceGroup              testase1-rg
    VnetName                       TestNetwork
    WebAppName                     vnetintdemoapp
    WebAppLocation                 centralus

이 섹션의 나머지 부분 hello 앞서 설명한 만든 변수 있다고 가정 합니다.

##### <a name="declare-hello-virtual-network-toohello-app"></a>Hello 가상 네트워크 toohello 앱 선언
다음 명령 tootell hello 앱을 사용할 것이 가상 네트워크는 hello를 사용 합니다. 이렇게 하면 hello 앱 toogenerate 필요한 인증서:

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -PropertyObject @{"VnetResourceId" = "/subscriptions/$($Configuration.VnetSubscriptionId)/resourceGroups/$($Configuration.VnetResourceGroup)/providers/Microsoft.ClassicNetwork/virtualNetworks/$($Configuration.VnetName)"} -Location $Configuration.WebAppLocation -ApiVersion 2015-07-01

이 명령이 성공하면 **$vnet**에는 **속성** 변수가 있어야 합니다. hello **속성** 변수 모두는 인증서 지문 및 hello 인증서 데이터를 포함 해야 합니다.

##### <a name="upload-hello-web-app-certificate-toohello-virtual-network"></a>Hello 웹 응용 프로그램 인증서 toohello 가상 네트워크를 업로드 합니다.
각 구독 및 가상 네트워크 조합에 일회성 수동 단계가 필요합니다. 즉, 구독 A tooVirtual 네트워크 A에서 응용 프로그램을 연결 하는 할 경우 toodo이이 단계 구성한 앱 수에 관계 없이 한 번만 합니다. 새 앱 tooanother 가상 네트워크를 추가 하는 경우 해야 toodo 다시 합니다. 이 대 한 hello 이유는 Azure 앱 서비스의 구독 수준에는 인증서 집합을 생성 하는 hello 집합 hello 앱에 연결 하는 각 가상 네트워크에 대해 한 번 생성 됩니다.

hello 인증서는 이미 설정 되어 다음이 단계를 따라 또는 통합 한 경우 hello로 동일 hello 포털을 사용 하 여 가상 네트워크입니다.

hello 첫 번째 단계는 toogenerate hello.cer 파일입니다. hello 두 번째 단계는 tooupload hello.cer 파일 tooyour 가상 네트워크입니다. toogenerate hello.cer 파일 hello에 hello API 호출에서 이전 단계를 hello 다음 명령을 실행 합니다.

    $certBytes = [System.Convert]::FromBase64String($vnet.Properties.certBlob)
    [System.IO.File]::WriteAllBytes("$($Configuration.GeneratedCertificatePath)", $certBytes)

hello 인증서 섹션 hello 위치는 **$Configuration.GeneratedCertificatePath** 지정 합니다.

tooupload hello 인증서를 직접 사용 하 여 hello [Azure 포털] [ azureportal] 및 **찾아보기 가상 네트워크 (클래식)** > **VPN연결**  >  **지점-사이트** > **인증서 관리**합니다. 여기에서 인증서를 업로드합니다.

##### <a name="get-hello-point-to-site-package"></a>Hello 지점 및 사이트 패키지 가져오기
웹 앱에 대 한 가상 네트워크 연결을 설정할 hello 다음 단계는 tooget hello 지점 및 사이트 패키지 하 고 tooyour 웹 응용 프로그램을 제공 합니다.

다음 예를 들어 C:\Azure\Templates\GetNetworkPackageUri.json 컴퓨터에 GetNetworkPackageUri.json 어딘가에 라는 템플릿 tooa 파일 hello를 저장 합니다.

    {
        "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "certData": {
                "type": "string"
            },
            "certThumbprint": {
                "type": "string"
            },
            "networkName": {
                "type": "string"
            }
        },
        "variables": {
            "legacyVnetName": "[concat('Group ', resourceGroup().name, ' ', parameters('networkName'))]"
            },
            "resources": [
            ],
        "outputs" : {
            "PackageUri" :
            {
            "value" : "[listPackage(resourceId('Microsoft.ClassicNetwork/virtualNetworks/gateways/clientRootCertificates', parameters('networkName'), 'primary', parameters('certThumbprint')), '2014-06-01').packageUri]", "type" : "string"
            }
        }
    }


입력 매개 변수 설정:

    $parameters = @{"certData" = $vnet.Properties.certBlob ;
    certThumbprint = $vnet.Properties.certThumbprint ;
    "networkName" = $Configuration.VnetName }

Hello 스크립트를 호출 합니다.

    $output = New-AzureRmResourceGroupDeployment -Name unused -ResourceGroupName $Configuration.VnetResourceGroup -TemplateParameterObject $parameters -TemplateFile C:\PATH\TO\GetNetworkPackageUri.json


hello 변수 **$output 합니다. Outputs.packageUri** tooyour 웹 응용 프로그램을 제공 하는 hello 패키지 URI toobe 포함 됩니다.

##### <a name="upload-hello-point-to-site-package-tooyour-app"></a>Hello 지점 및 사이트 패키지 tooyour 앱 업로드
hello 마지막 단계는이 패키지와 tooprovide hello 앱입니다. Hello 다음 명령을 실행 하면 됩니다.

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)/primary" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-07-01 -PropertyObject @{"VnetName" = $Configuration.VnetName ; "VpnPackageUri" = $($output.Outputs.packageUri).Value } -Location $Configuration.WebAppLocation

메시지가 기존 리소스를 덮어쓰는 tooconfirm를 묻는 확인 되었는지 tooallow 것입니다.

이 명령은 성공 하면 앱 가상 네트워크에 연결 된 toohello 됩니다. tooconfirm 성공 tooyour 응용 프로그램 콘솔을 hello 다음을 입력 합니다.

    SET WEBSITE_

Hello 대상 가상 네트워크의 hello 이름과 일치 하는 값을 가진 WEBSITE_VNETNAME 라는 환경 변수 이면 모든 구성에 성공 했습니다.

### <a name="update-classic-vnet-integration-information"></a>클래식 VNet 통합 정보 업데이트
tooupdate 또는 사용자의 정보를 다시 동기화, 단순히 hello 첫 번째 위치에서 hello 통합을 만들 때 수행한 hello 단계를 반복 합니다. 이러한 단계는 다음과 같습니다.

1. 구성 정보를 정의합니다.
2. Hello 가상 네트워크 toohello 앱을 선언 합니다.
3. Hello 지점 및 사이트 패키지를 가져옵니다.
4. Hello 지점 및 사이트 패키지 tooyour 앱을 업로드 합니다.

### <a name="disconnect-your-app-from-a-classic-vnet"></a>클래식 VNet에서 앱 연결을 끊습니다.
toodisconnect hello 앱 가상 네트워크 통합 하는 동안 설정 된 hello 구성 정보를 해야 합니다. 해당 정보를 사용 하는 하나의 명령 toodisconnect 다음 가상 네트워크에서 응용 프로그램

    $vnet = Remove-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-07-01

## <a name="resource-manager-virtual-networks"></a>리소스 관리자 가상 네트워크
리소스 관리자 가상 네트워크에는 클래식 가상 네트워크와 비교했을 때 일부 프로세스를 간소화하는 Azure Resource Manager API가 있습니다. Hello 다음 작업을 완료 하는 데 도움이 되는 스크립트를 해야 합니다.

* 리소스 관리자 가상 네트워크를 만들고 앱을 여기에 통합합니다.
* 게이트웨이를 만들고 기존 리소스 관리자 가상 네트워크에서 지점 및 사이트 간 연결을 구성 후 앱을 함께 통합합니다.
* 게이트웨이가 있고 지점 및 사이트 간 연결이 활성화된 기존 리소스 관리자 가상 네트워크와 앱을 통합합니다.
* 가상 네트워크에서 앱 연결을 끊습니다.

### <a name="resource-manager-vnet-app-service-integration-script"></a>리소스 관리자 VNet 앱 서비스 통합 스크립트
다음 스크립트를 tooa 파일을 저장 하는 hello를 복사 합니다. Toouse hello 스크립트를 사용 하지 않으려는 경우 느껴집니다 여기에서 무료 toolearn toosee 어떻게 tooset 리소스 관리자 가상 네트워크와 함께 작업 합니다.

    function ReadHostWithDefault($message, $default)
    {
        $result = Read-Host "$message [$default]"
        if($result -eq "")
        {
            $result = $default
        }
            return $result
        }

    function PromptCustom($title, $optionValues, $optionDescriptions)
    {
        Write-Host $title
        Write-Host
        $a = @()
        for($i = 0; $i -lt $optionValues.Length; $i++){
            Write-Host "$($i+1))" $optionDescriptions[$i]
        }
        Write-Host

        while($true)
        {
            Write-Host "Choose an option: "
            $option = Read-Host
            $option = $option -as [int]

            if($option -ge 1 -and $option -le $optionValues.Length)
            {
                return $optionValues[$option-1]
            }
        }
    }

    function PromptYesNo($title, $message, $default = 0)
    {
        $yes = New-Object System.Management.Automation.Host.ChoiceDescription "&Yes", ""
        $no = New-Object System.Management.Automation.Host.ChoiceDescription "&No", ""
        $options = [System.Management.Automation.Host.ChoiceDescription[]]($yes, $no)
        $result = $host.ui.PromptForChoice($title, $message, $options, $default)
        return $result
    }

    function CreateVnet($resourceGroupName, $vnetName, $vnetAddressSpace, $vnetGatewayAddressSpace, $location)
    {
        Write-Host "Creating a new VNET"
        $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
        New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location -AddressPrefix $vnetAddressSpace -Subnet $gatewaySubnet
    }

    function CreateVnetGateway($resourceGroupName, $vnetName, $vnetIpName, $location, $vnetIpConfigName, $vnetGatewayName, $certificateData, $vnetPointToSiteAddressSpace)
    {
        $vnet = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName
        $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet

        Write-Host "Creating a public IP address for this VNET"
        $pip = New-AzureRmPublicIpAddress -Name $vnetIpName -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
        $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $vnetIpConfigName -Subnet $subnet -PublicIpAddress $pip

        Write-Host "Adding a root certificate toothis VNET"
        $root = New-AzureRmVpnClientRootCertificate -Name "AppServiceCertificate.cer" -PublicCertData $certificateData

        Write-Host "Creating Azure VNET Gateway. This may take up tooan hour."
        New-AzureRmVirtualNetworkGateway -Name $vnetGatewayName -ResourceGroupName $resourceGroupName -Location $location -IpConfigurations $ipconf -GatewayType Vpn -VpnType RouteBased -EnableBgp $false -GatewaySku Basic -VpnClientAddressPool $vnetPointToSiteAddressSpace -VpnClientRootCertificates $root
    }

    function AddNewVnet($subscriptionId, $webAppResourceGroup, $webAppName)
    {
        Write-Host "Adding a new Vnet"
        Write-Host
        $vnetName = Read-Host "Specify a name for this Virtual Network"

        $vnetGatewayName="$($vnetName)-gateway"
        $vnetIpName="$($vnetName)-ip"
        $vnetIpConfigName="$($vnetName)-ipconf"

        # Virtual Network settings
        $vnetAddressSpace="10.0.0.0/8"
        $vnetGatewayAddressSpace="10.5.0.0/16"
        $vnetPointToSiteAddressSpace="172.16.0.0/16"

        $changeRequested = 0
        $resourceGroupName = $webAppResourceGroup

        while($changeRequested -eq 0)
        {
            Write-Host
            Write-Host "Currently, I will create a VNET with hello following settings:"
            Write-Host
            Write-Host "Virtual Network Name: $vnetName"
            Write-Host "Resource Group Name:  $resourceGroupName"
            Write-Host "Gateway Name: $vnetGatewayName"
            Write-Host "Vnet IP name: $vnetIpName"
            Write-Host "Vnet IP config name:  $vnetIpConfigName"
            Write-Host "Address Space:$vnetAddressSpace"
            Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
            Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
            Write-Host
            $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

            if($changeRequested -eq 0)
            {
                $vnetName = ReadHostWithDefault "Virtual Network Name" $vnetName
                $resourceGroupName = ReadHostWithDefault "Resource Group Name" $resourceGroupName
                $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                $vnetAddressSpace = ReadHostWithDefault "Vnet Address Space" $vnetAddressSpace
                $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
            }
        }

        $ErrorActionPreference = "Stop";

        # We create hello virtual network and add it here. hello way this works is:
        # 1) Add hello VNET association toohello App. This allows hello App toogenerate certificates, etc. for hello VNET.
        # 2) Create hello VNET and VNET gateway, add hello certificates, create hello public IP, etc., required for hello gateway
        # 3) Get hello VPN package from hello gateway and pass it back toohello App.

        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup
        $location = $webApp.Location

        Write-Host "Creating App association tooVNET"
        $propertiesObject = @{
         "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($resourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
        }
        $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        CreateVnet $resourceGroupName $vnetName $vnetAddressSpace $vnetGatewayAddressSpace $location

        CreateVnetGateway $resourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName -VirtualNetworkGatewayName $vnetGatewayName -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
        $PropertiesObject = @{
        "vnetName" = $VirtualNetworkName; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        Write-Host "Finished!"
    }

    function AddExistingVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $ErrorActionPreference = "Stop";

        # At this point, hello gateway should be able toobe joined tooan App, but may require some minor tweaking. We will declare toohello App now toouse this VNET
        Write-Host "Getting App information"
        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $location = $webApp.Location

        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected tooVNET $currentVnet"
        }

        # Display existing vnets
        $vnets = Get-AzureRmVirtualNetwork
        $vnetNames = @()
        foreach($vnet in $vnets)
        {
            $vnetNames += $vnet.Name
        }

        Write-Host
        $vnet = PromptCustom "Select a VNET toointegrate with" $vnets $vnetNames

        # We need toocheck if this VNET is able toobe joined tooa App, based on following criteria
            # If there is no gateway, we can create one.
            # If there is a gateway:
                # It must be of type Vpn
                # It must be of VpnType RouteBased
                # If it doesn't have hello right certificate, we will need tooadd it.
                # If it doesn't have a point-to-site range, we will need tooadd it.

        $gatewaySubnet = $vnet.Subnets | Where-Object { $_.Name -eq "GatewaySubnet" }

        if($gatewaySubnet -eq $null -or $gatewaySubnet.IpConfigurations -eq $null -or $gatewaySubnet.IpConfigurations.Count -eq 0)
        {
            $ErrorActionPreference = "Continue";
            # There is no gateway. We need toocreate one.
            Write-Host "This Virtual Network has no gateway. I will need toocreate one."

            $vnetName = $vnet.Name
            $vnetGatewayName="$($vnetName)-gateway"
            $vnetIpName="$($vnetName)-ip"
            $vnetIpConfigName="$($vnetName)-ipconf"

            # Virtual Network settings
            $vnetAddressSpace="10.0.0.0/8"
            $vnetGatewayAddressSpace="10.5.0.0/16"
            $vnetPointToSiteAddressSpace="172.16.0.0/16"

            $changeRequested = 0

            Write-Host "Your VNET is in hello address space $($vnet.AddressSpace.AddressPrefixes), with hello following Subnets:"
            foreach($subnet in $vnet.Subnets)
            {
                Write-Host "$($subnet.Name): $($subnet.AddressPrefix)"
            }

            $vnetGatewayAddressSpace = Read-Host "Please choose a GatewaySubnet address space"

            while($changeRequested -eq 0)
            {
                Write-Host
                Write-Host "Currently, I will create a VNET gateway with hello following settings:"
                Write-Host
                Write-Host "Virtual Network Name: $vnetName"
                Write-Host "Resource Group Name:  $($vnet.ResourceGroupName)"
                Write-Host "Gateway Name: $vnetGatewayName"
                Write-Host "Vnet IP name: $vnetIpName"
                Write-Host "Vnet IP config name:  $vnetIpConfigName"
                Write-Host "Address Space:$($vnet.AddressSpace.AddressPrefixes)"
                Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
                Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
                Write-Host
                $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

                if($changeRequested -eq 0)
                {
                    $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                    $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                    $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                    $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                    $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
                }
            }

            $ErrorActionPreference = "Stop";

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # If there is no gateway subnet, we need toocreate one.
            if($gatewaySubnet -eq $null)
            {
                $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
                $vnet.Subnets.Add($gatewaySubnet);
                Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
            }

            CreateVnetGateway $vnet.ResourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $vnetGatewayName
        }
        else
        {
            $uriParts = $gatewaySubnet.IpConfigurations[0].Id.Split('/')
            $gatewayResourceGroup = $uriParts[4]
            $gatewayName = $uriParts[8]

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $gatewayName

            # validate gateway types, etc.
            if($gateway.GatewayType -ne "Vpn")
            {
                Write-Error "This gateway is not of hello Vpn type. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnType -ne "RouteBased")
            {
                Write-Error "This gateways Vpn type is not RouteBased. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnClientConfiguration -eq $null -or $gateway.VpnClientConfiguration.VpnClientAddressPool -eq $null)
            {
                Write-Host "This gateway does not have a Point-to-site Address Range. Please specify one in CIDR notation, e.g. 10.0.0.0/8"
                $pointToSiteAddress = Read-Host "Point-To-Site Address Space"
                Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $gateway.Name -VpnClientAddressPool $pointToSiteAddress
            }

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnet.Name)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # We need toocheck if hello certificate here exists in hello gateway.
            $certificates = $gateway.VpnClientConfiguration.VpnClientRootCertificates

            $certFound = $false
            foreach($certificate in $certificates)
            {
                if($certificate.PublicCertData -eq $virtualNetwork.Properties.CertBlob)
                {
                    $certFound = $true
                    break
                }
            }

            if(-not $certFound)
            {
                Write-Host "Adding certificate"
                Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName "AppServiceCertificate.cer" -PublicCertData $virtualNetwork.Properties.CertBlob -VirtualNetworkGatewayName $gateway.Name
            }
        }

        # Now finish joining by getting hello VPN package and giving it toohello App
        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $vnet.ResourceGroupName -VirtualNetworkGatewayName $gateway.Name -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
        $PropertiesObject = @{
        "vnetName" = $vnet.Name; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

        Write-Host "Finished!"
    }

    function RemoveVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected tooVNET $currentVnet"

            Remove-AzureRmResource -ResourceName "$($webAppName)/$($currentVnet)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        }
            else
        {
            Write-Host "Not connected tooa VNET."
        }
    }

    Write-Host "Please Login"
    Login-AzureRmAccount

    # Choose subscription. If there's only one we will choose automatically

    $subs = Get-AzureRmSubscription
    $subscriptionId = ""

    if($subs.Length -eq 0)
    {
        Write-Error "No subscriptions bound toothis account."
        return
    }

    if($subs.Length -eq 1)
    {
        $subscriptionId = $subs[0].SubscriptionId
    }
    else
    {
        $subscriptionChoices = @()
        $subscriptionValues = @()

        foreach($subscription in $subs){
        $subscriptionChoices += "$($subscription.SubscriptionName) ($($subscription.SubscriptionId))";
        $subscriptionValues += ($subscription.SubscriptionId);
        }

        $subscriptionId = PromptCustom "Choose a subscription" $subscriptionValues $subscriptionChoices
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    $resourceGroup = Read-Host "Please enter hello Resource Group of your App"

    $appName = Read-Host "Please enter hello Name of your App"

    $options = @("Add a NEW Virtual Network tooan App", "Add an EXISTING Virtual Network tooan App", "Remove a Virtual Network from an App");
    $optionValues = @(0, 1, 2)
    $option = PromptCustom "What do you want toodo?" $optionValues $options

    if($option -eq 0)
    {
        AddNewVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 1)
    {
        AddExistingVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 2)
    {
        RemoveVnet $subscriptionId $resourceGroup $appName
    }

Hello 스크립트의 복사본을 저장 합니다. 이 문서에서는 V2VnetAllinOne.ps1라고 하지만 다른 이름을 사용할 수 있습니다. 이 스크립트에 대한 인수가 없습니다. 단순히 실행할 수 있습니다. hello 먼저 hello 스크립트 처리 해 toosign에 라는 메시지가 표시 됩니다. 에 로그인 한 후 hello 스크립트는 사용자 계정에 대 한 세부 정보를 가져오고 구독 목록을 반환 합니다. 자격 증명에 대 한 hello 요청을 세 지 않고, hello 초기 스크립트 실행은 다음과 같습니다.

    PS C:\Users\ccompy\Documents\VNET> .\V2VnetAllInOne.ps1
    Please Login

    Environment           : AzureCloud
    Account               : ccompy@microsoft.com
    TenantId              : 722278f-fef1-499f-91ab-2323d011db47
    SubscriptionId        : af5358e1-acac-2c90-a9eb-722190abf47a
    CurrentStorageAccount :

    Choose a subscription

    1) Demo Subscription (af5358e1-acac-2c90-a9eb-722190abf47a)
    2) MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)
    3) Purple Demo Subscription (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)

    Choose an option: 3

    Account      : ccompy@microsoft.com Environment  : AzureCloud Subscription : 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Tenant       : 722278f-fef1-499f-91ab-2323d011db47

    Hello 응용 프로그램의 리소스 그룹을 입력 하십시오: hcdemo rg hello 응용 프로그램의 이름을 입력 하십시오: v2vnetpowershell 하 신 toodo 원하는?

    1) 새 가상 네트워크 tooan 앱 추가
    2) 기존 가상 네트워크 tooan 앱 추가
    3) Remove a Virtual Network from an App

hello이이 단원의 나머지 부분에서는 이러한 세 가지 옵션에 설명 합니다.

### <a name="create-a-resource-manager-vnet-and-integrate-with-it"></a>리소스 관리자 VNet 만들기 및 통합
toocreate 및 사용 하 여 리소스 관리자 배포 모델을 hello와 응용 프로그램을 통합 하 여 새 가상 네트워크 선택 **1) 새 가상 네트워크 tooan 앱 추가**합니다. Hello 가상 네트워크의 hello 이름 하면이 메시지가 나타납니다. 필자의 경우 hello 설정을 뒤에서 볼 수 v2pshell hello 이름을 사용 합니다.

hello 스크립트는 생성 중인 hello 가상 네트워크에 대 한 hello 세부 정보를 제공 합니다. hello 값 중 하나를 변경할 수 있습니까 합니다. 이 예제에서는 실행 hello 다음 설정 된 가상 네트워크를 만들었습니다.

    Virtual Network Name:         v2pshell
    Resource Group Name:          hcdemo-rg
    Gateway Name:                 v2pshell-gateway
    Vnet IP name:                 v2pshell-ip
    Vnet IP config name:          v2pshell-ipconf
    Address Space:                10.0.0.0/8
    Gateway Address Space:        10.5.0.0/16
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):

Toochange hello 값을 입력 **Y** hello 변경 합니다. Hello 가상 네트워크 설정에 만족 하는 경우 입력 **N** 하거나 단순히 hello 설정을 변경 하는 방법에 대 한 메시지가 표시 되 면 Enter 키를 누릅니다. 대 완료 될 때까지 여기에서 hello 스크립트를 알려 줍니다 일부 어떤 it' i toocreate hello 가상 네트워크 게이트웨이 시작 되기 전까지 수행 합니다. 해당 단계 tooan 시간을 걸릴 수 있습니다. 이 단계 동안 진행률 표시기가 없습니다 있지만 hello 게이트웨이가 때 만들어짐 알 hello 스크립트 수 있습니다.

말할 hello 스크립트 작업을 마치면 **마침**합니다. 이 시점에서 hello 이름을 가진 리소스 관리자 가상 네트워크 및 선택한 설정 해야 합니다. 이 새로운 가상 네트워크도 앱과 통합됩니다.

### <a name="integrate-your-app-with-a-preexisting-resource-manager-vnet"></a>기존 리소스 관리자 VNet와 앱 통합
에 게이트웨이 또는 지점 및 사이트 연결 없는 리소스 관리자 가상 네트워크를 제공 하는 경우 기존 가상 네트워크와 통합 하는 경우 hello 스크립트를 설정 합니다입니다. Hello VNET에 이미 이러한 일 들을 설정 하는 경우 hello 스크립트 직선 toohello 응용 프로그램 통합을 이동 합니다. toostart이이 프로세스를 선택 하기만 하면 **2) 기존 가상 네트워크 tooan 앱 추가**합니다.

Hello에 있는 기존 리소스 관리자 가상 네트워크에 있는 경우에이 옵션은 사용할 앱과 동일한 구독 합니다. Hello 옵션을 선택한 후 리소스 관리자 가상 네트워크의 목록이 나타납니다.   

    Select a VNET toointegrate with

    1) v2demonetwork
    2) v2pshell
    3) v2vnetintdemo
    4) v2asenetwork
    5) v2pshell2

    Choose an option: 5

단순히 hello와 toointegrate 원하는 가상 네트워크를 선택 합니다. 지점 및 사이트 연결을 사용 하도록 설정 되어 있는 게이트웨이 이미 있는 경우 hello 스크립트 가상 네트워크에 앱을 간단히 통합 합니다. 게이트웨이 toospecify hello 게이트웨이 서브넷을 해야 합니다. 게이트웨이 서브넷은 가상 네트워크 주소 공간에 있어야 하고 다른 서브넷에 있을 수 없습니다. 게이트웨이가 없는 가상 네트워크가 있고 이 단계를 실행하는 경우 다음과 같습니다.

    This Virtual Network has no gateway. I will need toocreate one.
    Your VNET is in hello address space 172.16.0.0/16, with hello following Subnets:
    default: 172.16.0.0/24
    Please choose a GatewaySubnet address space: 172.16.1.0/26

이 예제에서는 hello 설정을 뒤에 있는 가상 네트워크 게이트웨이 만들었습니다.

    Virtual Network Name:         v2pshell2
    Resource Group Name:          vnetdemo-rg
    Gateway Name:                 v2pshell2-gateway
    Vnet IP name:                 v2pshell2-ip
    Vnet IP config name:          v2pshell2-ipconf
    Address Space:                172.16.0.0/16
    Gateway Address Space:        172.16.1.0/26
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):
    Creating App association tooVNET

Toochange, 이러한 설정을 사용할 경우이 수행할 수 있습니다. 그렇지 않은 경우 Enter 키를 누릅니다 및 hello 스크립트는 게이트웨이 만들고 앱 tooyour 가상 네트워크를 연결 합니다. hello 게이트웨이 만든 시간은 경우에 한 시간 여전히, 염두에서 계속가지고 있는지 확인 합니다. Hello 스크립트는 예를 들어 모든 항목 완료 되 면 **마침**합니다.

### <a name="disconnect-your-app-from-a-resource-manager-vnet"></a>리소스 관리자 VNet에서 앱 연결 끊기
가상 네트워크에서 응용 프로그램 연결을 해제 해도 hello 게이트웨이 작동 중지 하거나 지점 및 사이트 연결을 사용 하지 않도록 설정 하지 않습니다. 어차피 다른 용도로 사용할 수 있습니다. 것도 끊어지지 않습니다 것 hello 이외의 다른 앱에서 사용자가 제공한 하나. tooperform이이 작업을 선택 **3) 응용 프로그램에서 가상 네트워크를 제거**합니다. 이를 수행할 때 다음과 같이 표시됩니다.

    Currently connected tooVNET v2pshell

    Confirm
    Are you sure you want toodelete hello following resource:
    /subscriptions/edcc99a4-b7f9-4b5e-a9a1-3034c51db496/resourceGroups/hcdemo-rg/providers/Microsoft.Web/sites/v2vnetpowers
    hell/virtualNetworkConnections/v2pshell
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

Hello 스크립트 표시 되지만 delete을 hello 가상 네트워크는 삭제 되지 않습니다. 것 바로 제거 하는 hello 통합 합니다. 원하는 작업 인지 확인 한 후, toodo hello 명령 매우 신속 하 게 처리 되 고 알려 **True** 완료 되 면입니다.

<!--Links-->
[createvpngateway]: http://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/
[azureportal]: http://portal.azure.com
