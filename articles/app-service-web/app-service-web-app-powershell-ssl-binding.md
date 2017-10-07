---
title: "PowerShell을 사용 하 여 바인딩 aaaSSL 인증서"
description: "어떻게 toobind SSL 인증서 PowerShell을 사용 하 여 tooyour 웹 앱에 알아봅니다."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 8ce32508-e982-48d3-b878-0e526afda537
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: 82f0e7c796da99ab50f69f3638ef64d55a94fc8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a>PowerShell을 사용하여 Azure 앱 서비스 SSL 인증서 바인딩
Hello 릴리스의 Microsoft Azure PowerShell 버전 1.1.0 새 cmdlet이 추가 되었습니다 hello 사용자 hello 기능 toobind 기존 또는 새 SSL 인증서 tooan 기존 웹 앱을 가지게 됩니다.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

Azure 리소스 관리자를 사용 하는 방법에 대 한 toolearn 기반 Azure PowerShell cmdlet toomanage 웹 응용 프로그램 확인 [Azure 리소스 관리자 기반 Azure 웹 앱에 대 한 PowerShell 명령](app-service-web-app-azure-resource-manager-powershell.md)

## <a name="uploading-and-binding-a-new-ssl-certificate"></a>새 SSL 인증서 업로드 및 바인딩
시나리오: hello 사용자가 웹 응용 프로그램의는 SSL 인증서 tooone toobind를 것인지 합니다.

Hello hello 인증서에 대 한 암호 및 사용자 지정 호스트 이름을 hello hello 웹 응용 프로그램, hello 웹 응용 프로그램 이름, hello 사용자 컴퓨터에 hello 인증서.pfx 파일 경로 포함 하는 hello 리소스 그룹 이름을 알고 있으면, 다음 PowerShell 명령을 toocreate hello 사용할 수 있는 SSL 바인딩:

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

Note SSL 바인딩 tooa 웹 응용 프로그램을 추가 하기 전에 호스트 이름 (사용자 지정 도메인) 이미 구성 되어 있어야 합니다. Hello 호스트 이름이 구성 되지 않은 경우 오류가 발생 합니다 AzureRmWebAppSSLBinding 새로 만들기를 실행 하는 동안 'hostname'가 없습니다. Hello 포털 또는 Azure PowerShell을 사용 하 여에서 직접 호스트 이름을 추가할 수 있습니다. hello 다음 PowerShell 코드 조각을 수 tooconfigure hello hostname AzureRmWebAppSSLBinding 새로 만들기를 실행 하기 전에.   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

집합 AzureRmWebApp cmdlet hello toounderstand 덮어씁니다 hello 웹 앱에 대 한 호스트 이름을 hello 유용 합니다. 따라서 PowerShell 코드 조각 위에 hello hello 웹 앱에 대 한 hello 호스트 이름의 toohello 기존 목록을 추가 됩니다.  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a>기존 SSL 인증서 업로드 및 바인딩
시나리오: hello 사용자가 웹 응용 프로그램의 이전에 업로드 된 SSL 인증서 tooone toobind를 것인지 합니다.

가져올 수 있습니다 hello 인증서 목록에 이미 업로드 된 tooa 특정 리소스 그룹 hello 다음 명령을 사용 하 여

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

Note hello 인증서는 로컬 tooa 특정 위치 및 리소스 그룹, hello 사용자 toore 업로드 hello 인증서 필요 hello 구성 된 웹 앱이 다른 위치에 리소스 그룹 다른 hello의 인증서를 필요한 경우 

Hello 웹 응용 프로그램 이름, 인증서 지문을 hello 및 사용자 지정 호스트 이름을 hello hello 웹 앱을 포함 하는 hello 리소스 그룹 이름을 알고 있으면, 다음 PowerShell 명령을 toocreate hello에 해당 SSL 바인딩을 사용할 수 있습니다.

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a>기존 SSL 바인딩 삭제
시나리오: hello 사용자는 기존 SSL 바인딩을 toodelete를 것인지 합니다.

웹 응용 프로그램 이름, hello 및 사용자 지정 호스트 이름을 hello hello 웹 앱을 포함 하는 hello 리소스 그룹 이름을 알고 있으면, 다음 PowerShell 명령을 tooremove hello에 해당 SSL 바인딩을 사용할 수 있습니다.

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

Hello SSL 바인딩을 제거 된 hello 마지막는 해당 인증서를 사용 하 여 해당 위치에 바인딩 기본 hello 인증서에 의해 삭제 됩니다, 그리고 hello DeleteCertificate 옵션 tookeep hello 인증서 사용 하기 위해 hello 사용자 tookeep hello 인증서 선택

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a>참조
* [Azure 웹앱용 Azure Resource Manager 기반 PowerShell 명령](app-service-web-app-azure-resource-manager-powershell.md)
* [소개 tooApp 서비스 환경](app-service-app-service-environment-intro.md)
* [Azure 리소스 관리자로 Azure PowerShell 사용](../powershell-azure-resource-manager.md)

