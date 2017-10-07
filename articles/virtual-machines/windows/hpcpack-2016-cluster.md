---
title: "Azure에서 클러스터를 aaaHPC 팩 2016 | Microsoft Docs"
description: "Azure에서 HPC 팩 2016 toodeploy 클러스터링 하는 방법에 대해 알아봅니다"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3dde6a68-e4a6-4054-8b67-d6a90fdc5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/15/2016
ms.author: danlep
ms.openlocfilehash: 9e21ec70c822a783474b96da77ce925940279abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-hpc-pack-2016-cluster-in-azure"></a>Azure에서 HPC 팩 2016 클러스터 배포

이 문서 toodeploy에 hello 단계를 따라는 [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) Azure 가상 컴퓨터의 클러스터입니다. HPC Pack은 Microsoft Azure 및 Windows Server 기술로 구축된 Microsoft의 무료 HPC 솔루션으로, 광범위한 HPC 워크로드를 지원합니다.

Hello 중 하나를 사용 하 여 [Azure 리소스 관리자 템플릿을](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC 팩 2016 클러스터입니다. 클러스터 헤드 노드의 숫자가 다른 클러스터 토폴로지를 선택하고 Linux 또는 Windows 계산 노드를 사용할지 선택합니다.

## <a name="prerequisites"></a>필수 조건

### <a name="pfx-certificate"></a>PFX 인증서

Microsoft HPC Pack 2016 클러스터 hello HPC 노드 간의 정보 교환 PFX (개인) 인증서 toosecure hello 통신이 필요합니다. hello 인증서 요구 사항을 준수 하는 hello를 충족 해야 합니다.

* 키 교환이 가능한 개인 키가 있어야 함
* 디지털 서명 및 키 암호화를 포함하는 키 사용
* 클라이언트 인증 및 서버 인증을 포함하는 강화된 키 사용

이러한 요구 사항을 충족 하는 인증서를 아직 없는 경우에 인증 기관에서 hello 인증서를 요청할 수 있습니다. 또는 hello 명령을 toogenerate hello 자체 서명 된 인증서를 hello 명령을 실행 하 고이 hello PFX 형식 인증서 개인 키를 포함 하 여 내보낼 hello 운영 체제에 따라 다음을 사용할 수 있습니다.

* **Windows 10 또는 Windows Server 2016에 대 한**, 기본 제공 hello 실행 **New-selfsignedcertificate** 다음과 같이 PowerShell cmdlet:

  ```PowerShell
  New-SelfSignedCertificate -Subject "CN=HPC Pack 2016 Communication" -KeySpec KeyExchange -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2") -CertStoreLocation cert:\CurrentUser\My -KeyExportPolicy Exportable -NotAfter (Get-Date).AddYears(5)
  ```
* **운영 체제의 Windows 10 또는 Windows Server 2016 이전**, hello 다운로드 [자체 서명 된 인증서 생성기](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) hello Microsoft 스크립트 센터에서에서. 콘텐츠를 추출 하 고 다음 PowerShell 프롬프트에서 명령을 hello를 실행 합니다.

    ```PowerShell 
    Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
  
    New-SelfSignedCertificateEx -Subject "CN=HPC Pack 2016 Communication" -KeySpec Exchange -KeyUsage "DigitalSignature,KeyEncipherment" -EnhancedKeyUsage "Server Authentication","Client Authentication" -StoreLocation CurrentUser -Exportable -NotAfter (Get-Date).AddYears(5)
    ```

### <a name="upload-certificate-tooan-azure-key-vault"></a>인증서 tooan Azure 키 자격 증명 모음 업로드

Hello HPC 클러스터를 배포 하기 전에 hello 인증서 tooan 업로드 [Azure 키 자격 증명 모음](../../key-vault/index.md) 비밀을 및 레코드 hello hello 배포 중에 사용 하기 위해 정보를 다음으로: **자격 증명 모음 이름**, ** 자격 증명 모음 리소스 그룹**, **인증서 URL**, 및 **인증서 지문을**합니다.

샘플 PowerShell 스크립트 tooupload hello 인증서는 다음과 같습니다. 인증서 tooan Azure 키 자격 증명 모음에 업로드 하는 방법에 대 한 자세한 내용은 참조 [Azure 키 자격 증명 모음 시작](../../key-vault/key-vault-get-started.md)합니다.

```powershell
#Give hello following values
$VaultName = "mytestvault"
$SecretName = "hpcpfxcert"
$VaultRG = "myresourcegroup"
$location = "westus"
$PfxFile = "c:\Temp\mytest.pfx"
$Password = "yourpfxkeyprotectionpassword"
#Validate hello pfx file
try {
    $pfxCert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList $PfxFile, $Password
}
catch [System.Management.Automation.MethodInvocationException]
{
    throw $_.Exception.InnerException
}
$thumbprint = $pfxCert.Thumbprint
$pfxCert.Dispose()
# Create and encode hello JSON object
$pfxContentBytes = Get-Content $PfxFile -Encoding Byte
$pfxContentEncoded = [System.Convert]::ToBase64String($pfxContentBytes)
$jsonObject = @"
{
"data": "$pfxContentEncoded",
"dataType": "pfx",
"password": "$Password"
}
"@
$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)
#Create an Azure key vault and upload hello certificate as a secret
$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
$rg = Get-AzureRmResourceGroup -Name $VaultRG -Location $location -ErrorAction SilentlyContinue
if($null -eq $rg)
{
    $rg = New-AzureRmResourceGroup -Name $VaultRG -Location $location
}
$hpcKeyVault = New-AzureRmKeyVault -VaultName $VaultName -ResourceGroupName $VaultRG -Location $location -EnabledForDeployment -EnabledForTemplateDeployment
$hpcSecret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secret
"hello following Information will be used in hello deployment template"
"Vault Name             :   $VaultName"
"Vault Resource Group   :   $VaultRG"
"Certificate URL        :   $($hpcSecret.Id)"
"Certificate Thumbprint :   $thumbprint"

```


## <a name="supported-topologies"></a>지원되는 토폴로지

Hello 중 하나를 선택 [Azure 리소스 관리자 템플릿을](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC 팩 2016 클러스터입니다. 다음은 지원되는 세 가지 클러스터 토폴로지의 상위 수준 아키텍처입니다. 고가용성 토폴로지는 여러 클러스터 헤드 노드를 포함합니다.

1. Active Directory 도메인을 사용하는 고가용성 클러스터

    ![AD 도메인의 HA 클러스터](./media/hpcpack-2016-cluster/haad.png)



2. Active Directory 도메인을 사용하지 않는 고가용성 클러스터

    ![AD 도메인이 없는 HA 클러스터](./media/hpcpack-2016-cluster/hanoad.png)

3. 단일 헤드 노드를 포함한 클러스터

   ![단일 헤드 노드를 포함한 클러스터](./media/hpcpack-2016-cluster/singlehn.png)


## <a name="deploy-a-cluster"></a>클러스터 배포

toocreate hello 클러스터 서식 파일을 선택 하 고 클릭 **tooAzure 배포**합니다. Hello에 [Azure 포털](https://portal.azure.com), 단계를 수행 하는 hello에 설명 된 대로 hello 서식 파일에 대 한 매개 변수를 지정 합니다. 각 템플릿은 hello HPC 클러스터 인프라에 필요한 모든 Azure 리소스를 만듭니다. 리소스는 Azure 가상 네트워크, 공용 IP 주소, 부하 분산 장치(고가용성 클러스터만 해당), 네트워크 인터페이스, 가용성 집합, 저장소 계정 및 가상 컴퓨터를 포함합니다.

### <a name="step-1-select-hello-subscription-location-and-resource-group"></a>1 단계: hello 구독, 위치 및 리소스 그룹 선택

hello **구독** 및 hello **위치** PFX 인증서를 업로드 하는 경우 지정 된 동일 해야 합니다 (필수 구성 요소 참조). 만들어야 하는 것이 좋습니다는 **리소스 그룹** hello 배포에 대 한 합니다.

### <a name="step-2-specify-hello-parameter-settings"></a>2 단계: hello 매개 변수 설정 지정

입력 하거나 hello 템플릿 매개 변수 값을 수정 합니다. Hello 아이콘 다음 tooeach 매개 변수 도움말 정보에 대 한를 클릭 합니다. 또한 hello 지침을 참조 [사용 가능한 VM 크기](sizes.md)합니다.

Hello 매개 변수 뒤에 대 한 hello 필수 구성 요소에 기록 하는 hello 값을 지정: **자격 증명 모음 이름**, **자격 증명 모음 리소스 그룹**, **인증서 URL**, 및 **인증서 지문을**합니다.

### <a name="step-3-review-legal-terms-and-create"></a>3단계. 약관 검토 및 만들기
클릭 **약관을 검토** tooreview hello 용어입니다. 동의 하면 클릭 **구매**, 클릭 하 고 **만들기** toostart hello 배포 합니다.

## <a name="connect-toohello-cluster"></a>Toohello 클러스터에 연결
1. Hello HPC Pack 클러스터를 배포한 후 이동 toohello [Azure 포털](https://portal.azure.com)합니다. 클릭 **리소스 그룹**, 및 찾기 hello 리소스 그룹은 hello 클러스터 배포 되었습니다. Hello 헤드 노드 가상 컴퓨터를 찾을 수 있습니다.

    ![Hello 포털에서 클러스터 헤드 노드](./media/hpcpack-2016-cluster/clusterhns.png)

2. 헤드 노드를 하나 클릭 (고가용성 클러스터)를 클릭 hello 헤드 노드 중 하나입니다. **Essentials**, hello 공용 IP 주소 또는 hello 클러스터의 전체 DNS 이름을 찾을 수 있습니다.

    ![클러스터 연결 설정](./media/hpcpack-2016-cluster/clusterconnect.png)

3. 클릭 **연결** 에 원격 데스크톱을 사용 하 여 지정 된 관리자 사용자 이름으로는 hello 헤드 노드의 tooany toolog 합니다. Active Directory 도메인에 배포 된 hello 클러스터 있으면 hello 사용자 이름이 hello 폼의 <privateDomainName> \<adminUsername > (예를 들어 hpc.local\hpcadmin).

## <a name="next-steps"></a>다음 단계
* Tooyour 클러스터 작업을 제출 합니다. 참조 [작업 tooHPC Azure의 HPC Pack 클러스터 제출](hpcpack-cluster-submit-jobs.md) 및 [Azure Active Directory를 사용 하 여 Azure의 HPC 팩 2016 클러스터는 관리](hpcpack-cluster-active-directory.md)합니다.

