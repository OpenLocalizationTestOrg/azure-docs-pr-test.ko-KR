---
title: "Azure 클라우드 서비스에 원격 데스크톱 aaaEnable | Microsoft Docs"
description: "어떻게 tooconfigure azure 클라우드 서비스 응용 프로그램 tooallow 원격 데스크톱 연결"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: d3110ee8-6526-4585-aba5-d0bc9a713e9b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: b3c0180bf5ad29cb77e5303ccbd6f9ccc44b7b0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a>Azure 클라우드 서비스의 역할에 대해 원격 데스크톱 연결 사용

> [!div class="op_single_selector"]
> * [Azure 포털](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Azure 클래식 포털](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)

서비스 정의에 hello 원격 데스크톱 모듈을 포함 하 여 개발 하는 동안 원격 데스크톱 연결 사용자 역할에 사용할 수 또는 원격 데스크톱 확장 hello 통해 원격 데스크톱 tooenable를 선택할 수 있습니다. hello 선호 되는 방법은 toouse hello 원격 데스크톱 확장 hello tooredeploy 응용 프로그램 필요 없이 배포 된 후에 원격 데스크톱을 사용할 수 있습니다.

## <a name="configure-remote-desktop-from-hello-azure-classic-portal"></a>Hello Azure 클래식 포털에서에서 원격 데스크톱을 구성 합니다.
Azure 클래식 포털 hello hello 원격 데스크톱 확장 방법을 사용 하 여 hello 응용 프로그램을 배포 후에 원격 데스크톱을 사용할 수 있도록 합니다. hello **구성** 클라우드 서비스에 대 한 페이지 tooenable 원격 데스크톱을 사용 하면, tooconnect toohello 가상 컴퓨터를 사용 하는 변경 hello 로컬 관리자 계정, hello 인증서 인증에 사용 하 고 hello 설정 만료 날짜입니다.

1. 클릭 **클라우드 서비스**hello 클라우드 서비스의 hello 이름을 클릭 하 고 클릭 **구성**합니다.
2. Hello 클릭 **원격** hello 아래쪽 단추입니다.

    ![클라우드 서비스 원격](./media/cloud-services-role-enable-remote-desktop/CloudServices_Remote.png)

   > [!WARNING]
   > 처음으로 원격 데스크톱을 사용하도록 설정한 후 확인(확인 표시)을 클릭하면 모든 역할 인스턴스가 다시 시작됩니다. 다시 부팅 hello 인증서 사용 되는 tooencrypt hello 암호 tooprevent hello 역할에 설치 되어야 합니다. tooprevent 다시 시작을 [hello 클라우드 서비스에 대 한 인증서 업로드](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) 다음 toothis 대화를 반환 합니다.

3. **역할**선택, 선택 하거나 tooupdate hello 역할 **모든** 모든 역할에 대 한 합니다.
4. Hello 변경 내용이 다음 중 하나를 확인 합니다.

   * 원격 데스크톱을 선택 하는 hello tooenable **원격 데스크톱 사용** 확인란 합니다. 원격 데스크톱 확인란 선택을 취소 hello toodisable 합니다.
   * Toohello 역할 인스턴스에 원격 데스크톱 연결에서 계정 toouse을 만듭니다.
   * Hello 기존 계정에 대 한 hello 암호를 업데이트 합니다.
   * 인증에는 인증서를 업로드 toouse 선택 (사용 하 여 업로드 hello 인증서 **업로드** hello에 **인증서** 페이지) 하거나 새 인증서를 만듭니다.
   * 원격 데스크톱 구성을 hello hello 만료 날짜를 변경 합니다.

5. 구성 업데이트를 마치면 **확인** (확인 표시)을 클릭합니다.

## <a name="remote-into-role-instances"></a>원격으로 역할 인스턴스 액세스
Hello 역할에 원격 데스크톱을 사용 하도록 설정 하면 원격 다양 한 도구를 통해 역할 인스턴스로 됩니다.

hello Azure 클래식 포털에서에서 tooconnect tooa 역할 인스턴스:

1. 클릭 **인스턴스** tooopen hello **인스턴스** 페이지.
2. 원격 데스크톱이 구성된 역할 인스턴스를 선택합니다.
3. 클릭 **연결**, hello 지침 tooopen hello 바탕 화면을 따릅니다.
4. 클릭 **열려** 차례로 **연결** toostart hello 원격 데스크톱 연결 합니다.

### <a name="use-visual-studio-tooremote-into-a-role-instance"></a>Visual Studio tooremote 역할 인스턴스를 사용 하 여
Visual Studio의 서버 탐색기:

1. Hello 확장 **Azure** > **클라우드 서비스** > **[클라우드 서비스 이름]** 노드.
2. **스테이징** 또는 **프로덕션**을 확장합니다.
3. Hello 개별 역할을 확장 합니다.
4. Hello 역할 인스턴스 중 하나를 마우스 오른쪽 단추로 클릭 하 여, **원격 데스크톱을 사용 하 여 연결...** , hello 사용자 이름 및 암호를 입력 합니다.

![서버 탐색기 원격 데스크톱](./media/cloud-services-role-enable-remote-desktop/ServerExplorer_RemoteDesktop.png)

### <a name="use-powershell-tooget-hello-rdp-file"></a>PowerShell tooget hello RDP 파일을 사용 하 여
Hello를 사용할 수 있습니다 [Get-azureremotedesktopfile](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet tooretrieve hello RDP 파일입니다. 그런 다음 원격 데스크톱 연결 tooaccess hello 클라우드 서비스와 hello RDP 파일을 사용할 수 있습니다.

### <a name="programmatically-download-hello-rdp-file-through-hello-service-management-rest-api"></a>프로그래밍 방식으로 hello 서비스 관리 REST API를 통해 hello RDP 파일 다운로드
Hello를 사용할 수 있습니다 [RDP 파일 다운로드](https://msdn.microsoft.com/library/jj157183.aspx) REST 작업 toodownload hello RDP 파일입니다.

## <a name="tooconfigure-remote-desktop-in-hello-service-definition-file"></a>tooconfigure hello 서비스 정의 파일에 원격 데스크톱
이 방법을 사용 하면 개발 하는 동안 hello 응용 프로그램에 대 한 원격 데스크톱 tooenable 있습니다. 이 접근 방식에서는 암호화 된 암호 저장에서 서비스 구성 파일 및 모든 업데이트 toohello 원격 데스크톱 구성 해야 합니다 hello 응용 프로그램의 프로젝트를 재배포 합니다. Tooavoid 하려는 경우 원격 데스크톱 확장 hello를 사용 해야 이러한 단점이 기반 위에서 설명한 하는 방법.  

Visual Studio도 사용할 수 있습니다[원격 데스크톱 연결 설정](../vs-azure-tools-remote-desktop-roles.md) hello 서비스 정의 파일 접근 방식을 사용 합니다.  
다음 hello 단계 hello 변경 내용이 필요한 toohello 서비스 모델 파일 tooenable 원격 데스크톱에 설명 합니다. 게시가 진행되면 Visual Studio에서 이러한 변경을 자동으로 수행합니다.

### <a name="set-up-hello-connection-in-hello-service-model"></a>Hello 서비스 모델에서 hello 연결 설정
사용 하 여 hello **Imports** 요소 tooimport hello **RemoteAccess** 모듈과 hello **RemoteForwarder** 모듈 toohello [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) 파일입니다.

hello 서비스 정의 파일 있어야 다음 hello로 예제와 비슷한 toohello `<Imports>` 요소를 추가 합니다.

```xml
<ServiceDefinition name="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2013-03.2.0">
    <WebRole name="WebRole1" vmsize="Small">
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="Endpoint1" endpointName="Endpoint1" />
                </Bindings>
            </Site>
        </Sites>
        <Endpoints>
            <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
            <Import moduleName="Diagnostics" />
            <Import moduleName="RemoteAccess" />
            <Import moduleName="RemoteForwarder" />
        </Imports>
    </WebRole>
</ServiceDefinition>
```
hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) 파일은 다음 예제와 비슷한 toohello 수, hello 참고 `<ConfigurationSettings>` 및 `<Certificates>` 요소입니다. 지정 된 인증서 hello 해야 [toohello 클라우드 서비스 업로드](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service)합니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2013-03.2.0">
    <Role name="WebRole1">
        <Instances count="2" />
        <ConfigurationSettings>
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.Enabled" value="true" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountUsername" value="[name-of-user-account]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountEncryptedPassword" value="[base-64-encrypted-user-password]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountExpiration" value="[certificate-expiration]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteForwarder.Enabled" value="true" />
        </ConfigurationSettings>
        <Certificates>
            <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="[certificate-thumbprint]" thumbprintAlgorithm="sha1" />
        </Certificates>
    </Role>
</ServiceConfiguration>
```


## <a name="additional-resources"></a>추가 리소스
[어떻게 tooConfigure 클라우드 서비스](cloud-services-how-to-configure.md)
[클라우드 서비스 FAQ-원격 데스크톱](cloud-services-faq.md)
