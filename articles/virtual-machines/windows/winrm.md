---
title: "Azure VM에 대 한 WinRM 액세스를 aaaSet | Microsoft Docs"
description: "Hello 리소스 관리자 배포 모델에서 만든 Azure 가상 컴퓨터와 사용에 대 한 WinRM 액세스를 설정 합니다."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 9718e85b-d360-4621-90b8-0b0b84a21208
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/16/2016
ms.author: kasing
ms.openlocfilehash: 23d1d3a3065cbd8e4036be085c6d835cae36caae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-winrm-access-for-virtual-machines-in-azure-resource-manager"></a>Azure Resource Manager에서 가상 컴퓨터에 대한 WinRM 액세스 설정
## <a name="winrm-in-azure-service-management-vs-azure-resource-manager"></a>Azure 서비스 관리 및 Azure Resource Manager의 WinRM

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

* Hello Azure 리소스 관리자의 개요를 참조 하십시오이 [문서](../../azure-resource-manager/resource-group-overview.md)
* Azure 서비스 관리 및 Azure Resource Manager 간의 차이점에 대해서는 이 [문서](../../resource-manager-deployment-model.md)

hello hello 두 스택 간에 WinRM 구성 설정의 주요 차이점은 hello 인증서 hello VM에 설치 되는 방법을 합니다. Hello Azure 리소스 관리자 스택의 hello 인증서 hello 키 자격 증명 모음 리소스 공급자에서 관리 하는 리소스 그룹으로 모델링 됩니다. 따라서 hello 사용자 tooprovide 자신의 인증서가 필요 하 고 VM에서 사용 하기 전에 tooa 주요 자격 증명 모음에 업로드 합니다.

다음은 WinRM 연결에 VM tootake tooset 필요한 hello 단계

1. 주요 자격 증명 모음 만들기
2. 자체 서명된 인증서 만들기
3. 자체 서명 된 인증서 tooKey 자격 증명 모음에 업로드
4. Hello 키 자격 증명 모음에에서 자체 서명 된 인증서에 대 한 hello URL 가져오기
5. VM을 만드는 동안 자체 서명된 인증서 URL 참조

## <a name="step-1-create-a-key-vault"></a>1단계: 주요 자격 증명 모음 만들기
명령 toocreate hello 주요 자격 증명 모음 아래 hello를 사용할 수 있습니다.

```
New-AzureRmKeyVault -VaultName "<vault-name>" -ResourceGroupName "<rg-name>" -Location "<vault-location>" -EnabledForDeployment -EnabledForTemplateDeployment
```

## <a name="step-2-create-a-self-signed-certificate"></a>2단계: 자체 서명된 인증서 만들기
이 PowerShell 스크립트를 사용하여 자체 서명된 인증서를 만들 수 있습니다.

```
$certificateName = "somename"

$thumbprint = (New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation Cert:\CurrentUser\My -KeySpec KeyExchange).Thumbprint

$cert = (Get-ChildItem -Path cert:\CurrentUser\My\$thumbprint)

$password = Read-Host -Prompt "Please enter hello certificate password." -AsSecureString

Export-PfxCertificate -Cert $cert -FilePath ".\$certificateName.pfx" -Password $password
```

## <a name="step-3-upload-your-self-signed-certificate-toohello-key-vault"></a>3 단계: 키 자격 증명 모음에 자체 서명 된 인증서 toohello 업로드
1 단계에서 만든 hello 인증서 toohello 주요 자격 증명 모음 업로드, 전에 tooconverted 형식 hello Microsoft.Compute 리소스 공급자는 이해 하는에 필요 합니다. 이렇게 하면 아래 PowerShell 스크립트는 hello 사용 하면

```
$fileName = "<Path toohello .pfx file>"
$fileContentBytes = Get-Content $fileName -Encoding Byte
$fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

$jsonObject = @"
{
  "data": "$filecontentencoded",
  "dataType" :"pfx",
  "password": "<password>"
}
"@

$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText –Force
Set-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>" -SecretValue $secret
```

## <a name="step-4-get-hello-url-for-your-self-signed-certificate-in-hello-key-vault"></a>4 단계: 키 자격 증명 모음 hello에 자체 서명 된 인증서에 대 한 hello URL 가져오기
hello Microsoft.Compute 리소스 공급자는 hello 키 자격 증명 모음 내 URL toohello 비밀 hello VM을 프로 비전 할 때 필요 합니다. 이 hello Microsoft.Compute 리소스 공급자 toodownload hello 암호를 사용 하도록 설정 하 고 hello VM에 hello 해당 인증서를 만듭니다.

> [!NOTE]
> hello 암호의 hello URL tooinclude hello 버전도 필요합니다. 예제 URL은 아래의 https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve 같은 형태
> 
> 

#### <a name="templates"></a>템플릿
아래 코드는 hello를 사용 하 여 hello 템플릿을에서 hello 링크 toohello URL을 확인할 수 있습니다.

    "certificateUrl": "[reference(resourceId(resourceGroup().name, 'Microsoft.KeyVault/vaults/secrets', '<vault-name>', '<secret-name>'), '2015-06-01').secretUriWithVersion]"

#### <a name="powershell"></a>PowerShell
아래의 PowerShell 명령 hello를 사용 하 여이 URL을 가져올 수 있습니다.

    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id

## <a name="step-5-reference-your-self-signed-certificates-url-while-creating-a-vm"></a>5단계: VM을 만드는 동안 자체 서명된 인증서 URL 참조
#### <a name="azure-resource-manager-templates"></a>Azure 리소스 관리자 템플릿
템플릿을 통해 VM을 만드는 동안 hello 비밀 섹션과 hello winRM 섹션 아래와 같이 hello 인증서 참조를 가져옵니다.

    "osProfile": {
          ...
          "secrets": [
            {
              "sourceVault": {
                "id": "<resource id of hello Key Vault containing hello secret>"
              },
              "vaultCertificates": [
                {
                  "certificateUrl": "<URL for hello certificate you got in Step 4>",
                  "certificateStore": "<Name of hello certificate store on hello VM>"
                }
              ]
            }
          ],
          "windowsConfiguration": {
            ...
            "winRM": {
              "listeners": [
                {
                  "protocol": "http"
                },
                {
                  "protocol": "https",
                  "certificateUrl": "<URL for hello certificate you got in Step 4>"
                }
              ]
            },
            ...
          }
        },

위의 hello에 대 한 샘플 템플릿을 확인할 수 있습니다에 [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)

이 템플릿의 소스 코드는 [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)

#### <a name="powershell"></a>PowerShell
    $vm = New-AzureRmVMConfig -VMName "<VM name>" -VMSize "<VM Size>"
    $credential = Get-Credential
    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName "<Computer Name>" -Credential $credential -WinRMHttp -WinRMHttps -WinRMCertificateUrl $secretURL
    $sourceVaultId = (Get-AzureRmKeyVault -ResourceGroupName "<Resource Group name>" -VaultName "<Vault Name>").ResourceId
    $CertificateStore = "My"
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore $CertificateStore -CertificateUrl $secretURL

## <a name="step-6-connecting-toohello-vm"></a>6 단계: toohello VM 연결
Toohello VM을 연결 하려면 먼저 toomake WinRM 원격 관리에 대 한 시스템 구성 되어 있는지 필요 합니다. 관리자 권한으로 PowerShell을 시작 하 고 설정 되어 있는지 명령 toomake 아래 hello를 실행 합니다.

    Enable-PSRemoting -Force

> [!NOTE]
> Toomake hello 위의 작동 하지 않을 경우 hello WinRM 서비스가 실행 되 고 있는지를 할 수 있습니다. 이 작업은 `Get-Service WinRM`
> 
> 

Hello 설치가 완료 되 면 VM toohello 연결할 수 있습니다 명령 아래의 hello를 사용 하 여

    Enter-PSSession -ConnectionUri https://<public-ip-dns-of-the-vm>:5986 -Credential $cred -SessionOption (New-PSSessionOption -SkipCACheck -SkipCNCheck -SkipRevocationCheck) -Authentication Negotiate
