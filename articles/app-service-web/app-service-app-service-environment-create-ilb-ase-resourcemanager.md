---
title: "aaaHow tooCreate는 ILB ASE를 사용 하 여 Azure 리소스 관리자 템플릿을 | Microsoft Docs"
description: "내부 프로그램 toocreate Azure 리소스 관리자 템플릿을 사용 하 여 분산 ASE를 로드 하는 방법에 대해 알아봅니다."
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 091decb6-b0de-42a1-9f2f-c18d9b2e67df
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: stefsch
ms.openlocfilehash: 16db20eccc232ccc73107fcc8291de180fb2a323
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-ilb-ase-using-azure-resource-manager-templates"></a>어떻게 tooCreate는 ILB ASE를 사용 하 여 Azure 리소스 관리자 템플릿

> [!NOTE] 
> 앱 서비스 환경 v1 hello에 대 한이 문서는입니다. 최신 버전의 hello 쉽게 toouse 되며 더 강력한 인프라에서 실행 하는 앱 서비스 환경 있습니다. hello로 시작 하는 hello 새 버전에 대 한 자세한 toolearn [소개 toohello 앱 서비스 환경](../app-service/app-service-environment/intro.md)합니다.
>

## <a name="overview"></a>개요
앱 서비스 환경은 공용 VIP 대신 가상 네트워크 내부 주소를 사용하여 만들 수 있습니다.  이러한 내부 주소는 hello 내부 부하 분산 장치 (ILB) 호출 하는 Azure 구성 요소에서 제공 됩니다.  ILB ASE hello Azure 포털을 사용 하 여 만들 수 있습니다.  Azure Resource Manager 템플릿을 통해 자동화 방식으로 만들 수도 있습니다.  이 문서에서는 hello 단계를 안내 하 고 구문 toocreate Azure 리소스 관리자 템플릿으로 ILB ASE를 필요 합니다.

ILB ASE 생성을 자동화하는 과정은 세 단계로 진행됩니다.

1. 첫 번째 hello 기본 ASE 공용 VIP 대신 내부 부하 분산 장치 주소를 사용 하 여 가상 네트워크에 생성 됩니다.  이 단계의 일부로 루트 도메인 이름은 toohello ILB ASE 할당 됩니다.
2. Hello ILB ASE를 만든 SSL 인증서를 업로드 합니다.  
3. hello 업로드 된 SSL 인증서가 명시적으로 할당 toohello ILB ASE "default" SSL 인증서로 합니다.  이 SSL 인증서에 사용할 SSL 트래픽 tooapps hello ILB ASE에 hello 공통 루트 할당 도메인 toohello (예: https://someapp.mycustomrootcomain.com) ASE를 사용 하 여 hello 응용 프로그램은 해결 되 면

## <a name="creating-hello-base-ilb-ase"></a>Hello 자료 ILB ASE 만들기
Azure Resource Manager 템플릿 예제 및 관련 매개 변수 파일은 GitHub의 [여기][quickstartilbasecreate]에서 사용할 수 있습니다.

Hello의 hello 매개 변수 대부분 *azuredeploy.parameters.json* 파일 일반적인 toocreating 두 ILB ASEs 뿐만 아니라 ASEs 바인딩된 tooa 공용 VIP 됩니다.  out 매개 변수 관련 참고의 호출 아래 hello 목록 또는 하는 고유한 ILB ASE를 만들 때:

* *interalLoadBalancingMode*: 대부분의 경우에서 포트 80/443에서 두 HTTP/HTTPS 트래픽을 즉이 too3 설정 및 hello 컨트롤/데이터 채널 포트 수신에 hello ASE tooby hello FTP 서비스, 바인딩된 tooan ILB 할당 될 가상 네트워크 내부 주소입니다.  이 속성은 유일한 hello FTP 서비스를 관련 된 포트 (둘 다 제어 및 데이터 채널)이 바인딩될 too2, 설정 대신 tooan ILB 주소, 동안 hello HTTP/HTTPS 트래픽을 hello 공용 VIP에 그대로 남아 있게 됩니다.
* *dnsSuffix*:이 매개 변수 hello toohello ASE 할당할 수 있는 기본 루트 도메인을 정의 합니다.  Azure 앱 서비스의 공용 변형을 hello hello 기본 루트 도메인 모든 웹 앱에 대 한는 *azurewebsites.net*합니다.  그러나 ILB ASE 내부 tooa 고객의 가상 네트워크 이므로, 것 의미 toouse hello 공용 서비스 기본 루트 도메인으로 확인 하지 않습니다.  대신, ILB ASE에는 회사의 내부 가상 네트워크 내에서 사용하기 적합한 기본 루트 도메인이 있어야 합니다.  가상 Contoso Corporation의 기본 루트 도메인을 사용할 수는 예를 들어 *내부 contoso.com* tooonly 의도 하는 응용 프로그램을 통해 확인 및 Contoso 가상 네트워크 내에서 액세스할 수 여야 합니다. 
* *ipSslAddressCount*:이 매개 변수는 자동으로 tooa hello에 0 값을 기본값으로 설정 *azuredeploy.json* ILB ASEs 단일 ILB 주소 하나만 있으므로 파일입니다.  ILB ASE에 대 한 명시적 IP SSL 주소가 없습니다. 있으며 따라서 hello ILB ASE에 대 한 IP SSL 주소 풀을 설정 해야 toozero, 그렇지 않으면 프로 비전 오류가 발생 합니다. 

한 번 hello *azuredeploy.parameters.json* 파일 채워진에 대 한 ILB ASE hello hello 다음 Powershell 코드 조각을 사용 하 여 ILB ASE을 만들 수 있습니다.  Hello 파일 경로 toomatch hello Azure 리소스 관리자 템플릿 파일이 컴퓨터에 위치를 변경 합니다.  또한 toosupply hello Azure 리소스 관리자 배포 이름 및 리소스 그룹 이름에 대 한 고유한 값을 기억 합니다.

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Hello Azure 리소스 관리자 후 서식 파일 전송 되는 hello ILB ASE toobe 생성에 대 한 몇 시간이 소요 됩니다.  Hello 생성 되 면 hello ILB ASE hello 포털 UX hello hello 배포를 트리거한 hello 구독에 대 한 앱 서비스 환경 목록에에서 표시 됩니다.

## <a name="uploading-and-configuring-hello-default-ssl-certificate"></a>업로드 하 고 hello "기본" SSL 인증서 구성
한 번 만든 ILB ASE hello, SSL 인증서를 연결 해야 할지 hello ASE SSL 연결 tooapps 설정 하기 위한 기본"hello" SSL 인증서 사용 합니다.  접미사는 hello ASE의 기본 DNS 경우 hello 가상 Contoso Corporation 예제를 계속 *내부 contoso.com*, 연결 후 너무*https://some-random-app.internal-contoso.com*에 유효한 SSL 인증서가 필요 **.internal contoso.com*합니다. 

내부 Ca를 포함 하는 외부 발급자 로부터 인증서를 구매 하 고 자체 서명 된 인증서를 사용 하 여 유효한 SSL 인증서는 다양 한 방법으로 tooobtain 합니다.  Hello SSL 인증서의 hello 소스에 관계 없이 hello 다음 인증서 특성 필요 toobe 올바르게 구성.

* *제목*:이 속성을 너무 설정 되어야 합니다. **루트 도메인 here.com.your*
* *주체 대체 이름*:이 특성이 모두 포함 해야 합니다 **루트 도메인 here.com.your*, 및 **.scm.your-루트-도메인-here.com*합니다.  hello hello 두 번째 항목에 대 한 이유는 각 앱과 연결 된 SCM/Kudu 사이트 걸 수 hello 폼의 주소를 사용 하는 SSL 연결 toohello *your-app-name.scm.your-root-domain-here.com*합니다.

유효한 SSL 인증서가 있는 경우 두 가지 추가 준비 단계가 필요합니다.  hello SSL 인증서를.pfx 파일로 변환/저장 toobe가 되어야 합니다.  반드시 해당 hello.pfx 파일 tooinclude 모든 중간 및 루트 인증서가 필요 하 고는 암호로 보호 toobe에도 필요 합니다.

그런 다음 hello 결과.pfx 파일 toobe Azure 리소스 관리자 템플릿을 사용 하 여 hello SSL 인증서를 업로드할 수는 때문에 base64 문자열로 변환 해야 합니다.  Azure 리소스 관리자 템플릿을 텍스트 파일, toobe hello 서식 파일의 매개 변수로 포함 될 수 있도록 base64 문자열로 변환 hello.pfx 파일이 필요 합니다.

아래 hello Powershell 코드 조각 자체 서명 된 인증서를 생성 하는 모양의 예제가 나와 hello 인증서 내보내기.pfx 파일로 hello.pfx 파일로 변환 하는 base64 인코딩 문자열입니다로 인코딩된 문자열 tooa 별도 파일을 다음 hello base64를 저장 합니다.  hello에서 변형 되었습니다 base64 인코딩을 대 한 Powershell 코드를 hello [Powershell 스크립트 블로그][examplebase64encoding]합니다.

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "*.internal-contoso.com","*.scm.internal-contoso.com"

    $certThumbprint = "cert:\localMachine\my\" + $certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText

    $fileName = "exportedcert.pfx"
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password     

    $fileContentBytes = get-content -encoding byte $fileName
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
    $fileContentEncoded | set-content ($fileName + ".b64")

Hello SSL 인증서가 성공적으로 생성 하 고 변환 된 tooa base64 인코딩된 문자열을 hello에 대 한 GitHub의 예제에서는 Azure Resource Manager 템플릿 [hello 기본 SSL 인증서 구성] [ configuringDefaultSSLCertificate] 사용할 수 있습니다.

hello에 대 한 매개 변수를 hello *azuredeploy.parameters.json* 파일은 다음과 같습니다.

* *appServiceEnvironmentName*: hello 구성 되 고 ILB ASE의 hello 이름입니다.
* *existingAseLocation*: hello ILB ASE를 배포할 Azure 지역 hello 포함 된 텍스트 문자열입니다.  예를 들어 "미국 중남부"입니다.
* *pfxBlobString*: hello based64 인코딩된 hello.pfx 파일의 문자열 표현입니다.  앞에서 살펴본 hello 코드 조각을 사용 하 여, "exportedcert.pfx.b64"에 포함 된 hello 문자열을 복사 하는 hello의 hello 값으로 붙여 *pfxBlobString* 특성입니다.
* *암호*: hello 사용 되는 암호 toosecure hello.pfx 파일입니다.
* *certificateThumbprint*: hello 인증서의 지문입니다.  Powershell에서이 값을 검색 하는 경우 (예: *$certificate 합니다. 지문* hello에서 이전 코드 조각의), hello 값으로 사용할 수 있습니다-됩니다.  그러나 hello Windows 인증서 대화 상자에서 hello 값을 복사 하는 경우 불필요 한 공백 hello 아웃 toostrip을 기억 합니다.  hello *certificateThumbprint* 다음과 같아야 합니다: AF3143EB61D43F6727842115BB7F17BBCECAECAE
* *certificateName*: tooidentity hello 인증서를 사용 하는 사용자가 선택한의 문자열 식별자입니다.  hello 이름이 hello에 대 한 hello 고유 Azure 리소스 관리자 식별자의 일부로 사용 됩니다 *Microsoft.Web/certificates* hello SSL 인증서를 나타내는 엔터티입니다.  hello 이름 **해야** hello 접미사를 다음으로 끝나는: \_yourASENameHere_InternalLoadBalancingASE 합니다.  이 접미사는 hello 포털에서 사용 표시기 hello 인증서를 ILB 사용이 가능한 ASE를 보안에 사용 됩니다.

*azuredeploy.parameters.json* 을 축약한 예는 다음과 같습니다.

    {
         "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json",
         "contentVersion": "1.0.0.0",
         "parameters": {
              "appServiceEnvironmentName": {
                   "value": "yourASENameHere"
              },
              "existingAseLocation": {
                   "value": "East US 2"
              },
              "pfxBlobString": {
                   "value": "MIIKcAIBAz...snip...snip...pkCAgfQ"
              },
              "password": {
                   "value": "PASSWORDGOESHERE"
              },
              "certificateThumbprint": {
                   "value": "AF3143EB61D43F6727842115BB7F17BBCECAECAE"
              },
              "certificateName": {
                   "value": "DefaultCertificateFor_yourASENameHere_InternalLoadBalancingASE"
              }
         }
    }

한 번 hello *azuredeploy.parameters.json* 파일 채워진, 다음 Powershell 코드 조각을 hello를 사용 하 여 hello 기본 SSL 인증서를 구성할 수 있습니다.  Hello 파일 경로 toomatch hello Azure 리소스 관리자 템플릿 파일이 컴퓨터에 위치를 변경 합니다.  또한 toosupply hello Azure 리소스 관리자 배포 이름 및 리소스 그룹 이름에 대 한 고유한 값을 기억 합니다.

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

후 hello Azure 리소스 관리자 템플릿은 분이 걸립니다 대략 40 분 ASE 프런트 엔드 tooapply hello 변경 당 제출 합니다.  예를 들어 기본값 두 프런트 엔드가 사용 하 여 크기의 ASE hello 템플릿을 걸립니다 1 시간 및 20 분 toocomplete.  Hello 템플릿 실행 되는 동안 hello ASE 수 tooscaled 되지 않습니다.  

Hello 템플릿 완료 되 면 앱 ILB ASE hello에 HTTPS를 통해 액세스할 수 있으며 hello 기본 SSL 인증서를 사용 하 여 hello 연결이 보호 됩니다.  hello 응용 프로그램 이름과 hello 기본 호스트 이름 조합을 사용 하 여 hello ILB ASE에 응용 프로그램은 해결 되 면 hello 기본 SSL 인증서 사용 됩니다.  예를 들어 *https://mycustomapp.internal-contoso.com* hello 기본 SSL 인증서에 대 한 사용 **.internal contoso.com*합니다.

그러나 hello 공개 하는 다중 테 넌 트 서비스에서 실행 중인 앱에서와 마찬가지로 개발자 개별 앱에 대 한 사용자 지정 호스트 이름을 구성할 수도 구성 하는 다음 개별 앱에 대 한 SNI SSL 인증서 바인딩을 고유 합니다.  

## <a name="getting-started"></a>시작
앱 서비스 환경 시작 tooget 참조 [소개 tooApp 서비스 환경](app-service-app-service-environment-intro.md)

모든 문서와 방법을-hello에서 사용할 수 있는 앱 서비스 환경에 대 한의 하려면 [응용 프로그램 서비스 환경에 대 한 추가 정보](../app-service/app-service-app-service-environments-readme.md)합니다.

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[quickstartilbasecreate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-create/
[examplebase64encoding]: http://powershellscripts.blogspot.com/2007/02/base64-encode-file.html 
[configuringDefaultSSLCertificate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl/ 

