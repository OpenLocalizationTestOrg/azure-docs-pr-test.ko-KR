---
title: "Azure CLI와 Azure 응용 프로그램에 대 한 aaaCreate id | Microsoft Docs"
description: "Toouse Azure CLI toocreate Azure Active Directory 응용 프로그램 및 서비스 사용자 및 역할 기반 액세스를 통해 tooresources 액세스용 부여 제어 하는 방법에 대해 설명 합니다. 표시 방법을 tooauthenticate 응용 프로그램 암호 또는 인증서를 사용 합니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c224a189-dd28-4801-b3e3-26991b0eb24d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 0d693ec801d4f4d6c24ec420580776e73014b325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-cli-toocreate-a-service-principal-tooaccess-resources"></a>Azure CLI toocreate 서비스 보안 주체 tooaccess 리소스 사용

응용 프로그램 또는 스크립트를 tooaccess 리소스가 필요한 경우 hello 앱에 대 한 id를 설정할 수 있으며 자체 자격 증명으로 hello 앱을 인증 합니다. 이 ID를 서비스 주체라고 합니다. 이 접근 방법을 사용하면 다음을 수행할 수 있습니다.

* 권한을 자신만 사용 권한을 것과 다른 toohello 응용 프로그램 id를 할당 합니다. 일반적으로 이러한 권한은 제한 된 tooexactly 어떤 hello 앱 toodo 필요 합니다.
* 무인 스크립트를 실행할 때 인증을 위해 인증서를 사용합니다.

이 문서에서는 어떻게 toouse [Azure CLI 1.0](../cli-install-nodejs.md) tooset 자체 자격 증명 및 identity는 응용 프로그램 toorun 합니다. 최신 버전의 hello 설치 [Azure CLI 1.0](../cli-install-nodejs.md) toomake 사용자 환경에이 문서의 hello 예제와 일치 하는지 확인 합니다.

## <a name="required-permissions"></a>필요한 사용 권한
toocomplete이이 항목에서는 Azure Active Directory와 Azure 구독에서 충분 한 권한이 있어야 합니다. 특히 수 toocreate hello Azure Active Directory에에서는 앱이 될 하 고 hello 서비스 보안 주체 tooa 역할을 할당 해야 합니다. 

hello 가장 쉬운 방법은 toocheck hello 포털을 통해이 계정을 적절 한 사용 권한이 있는지 여부. [포털에서 필요한 사용 권한 확인](resource-group-create-service-principal-portal.md#required-permissions)을 참조하세요.

이제 tooa 섹션 중 하나에 대 한 진행 [암호](#create-service-principal-with-password) 또는 [인증서](#create-service-principal-with-certificate) 인증 합니다.

## <a name="create-service-principal-with-password"></a>암호를 사용하여 서비스 주체 만들기
이 섹션에서는 hello 단계 toocreate hello AD 응용 프로그램 암호를 사용 하 여 수행 하 고 hello 판독기 toohello 서비스 사용자 역할을 할당 합니다.

1. Tooyour 계정에 로그인 합니다.
   
   ```azurecli
   azure login
   ```
2. toocreate 앱 id를 다음 명령을 hello와 같이 hello 앱의 hello 이름 및 암호를 제공 합니다.
     
   ```azurecli
   azure ad sp create -n exampleapp -p {your-password}
   ```
     
   hello 새 서비스 사용자가 반환 됩니다. hello 개체 Id 사용 권한을 부여할 때 필요 합니다. 서비스 사용자 이름 hello로 나열 된 hello guid 로그인 할 때 필요 합니다. 이 guid는 hello hello 응용 프로그램 id와 동일한 값입니다. Hello 샘플 응용 프로그램에서이 값은 참조 tooas hello `Client ID`합니다. 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating application exampleapp
     / Creating service principal for application 7132aca4-1bdb-4238-ad81-996ff91d8db+
     data:    Object Id:               ff863613-e5e2-4a6b-af07-fff6f2de3f4e
     data:    Display Name:            exampleapp
     data:    Service Principal Names:
     data:                             7132aca4-1bdb-4238-ad81-996ff91d8db4
     data:                             https://www.contoso.org/example
     info:    ad sp create command OK
   ```

3. 구독에 대해 hello 서비스 보안 주체 권한을 부여 합니다. 이 예제에서는 권한을 tooread hello 구독에 있는 모든 리소스 수 있게 하는 hello 서비스 보안 주체 toohello Reader 역할에 추가 합니다. 다른 역할에 대해서는 [RBAC: 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md)을 참조하세요. Hello objectid 매개 변수에 대 한 hello hello 응용 프로그램을 만들 때 사용한 개체 Id를 제공 합니다. 이 명령은 실행 하기 전에 Azure Active Directory 전체 hello 제공 하는 서비스 새 주 toopropagate 약간의 시간이 허용 해야 합니다. 이러한 명령을 수동으로 실행할 때 작업 간에 충분 한 시간이 경과되었습니다. 스크립트에는 단계 toosleep hello 명령 사이 추가 해야 (같은 `sleep 15`). 보안 주체는 오류 상자가 hello hello 디렉터리에 존재 하지 않는 표시 되 면 hello 명령을 다시 실행 하십시오.
   
   ```azurecli
   azure role assignment create --objectId ff863613-e5e2-4a6b-af07-fff6f2de3f4e -o Reader -c /subscriptions/{subscriptionId}/
   ```
   
이것으로 끝입니다. AD 응용 프로그램 및 서비스 주체가 설정되었습니다. hello 다음 섹션에서는 Azure CLI를 통해 toolog hello 사용 하 여 자격 증명 하는 방법을 보여 줍니다. 응용 프로그램 코드에서에서 toouse hello 자격 증명을 하려는 경우에이 항목을 toocontinue를 설치할 필요가 없습니다. Toohello를 건너뛸 수 있는 [샘플 응용 프로그램](#sample-applications) 응용 프로그램 id와 암호를 사용 하 여 로깅에 대 한 예제입니다. 

### <a name="provide-credentials-through-azure-cli"></a>Azure CLI를 통해 자격 증명 제공
이제, hello 응용 프로그램 tooperform 작업으로 toolog에 필요 합니다.

1. 서비스 사용자로 로그인 할 때마다 AD 앱에 대 한 hello 디렉터리의 tooprovide hello 테 넌 트 id가 필요 합니다. 테넌트는 Azure Active Directory의 인스턴스입니다. 현재 인증 된 구독을 사용 하 여에 대 한 tooretrieve hello 테 넌 트 id:
   
   ```azurecli
   azure account show
   ```
   
   반환하는 내용은 다음과 같습니다.
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
     Tooget hello 테 넌 트 id는 다른 구독 해야 할 경우 다음 명령을 hello를 사용 합니다.
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. 로그인 하기 위한 tooretrieve hello 클라이언트 id toouse 해야 할 경우 사용 합니다.
   
   ```azurecli
   azure ad sp show -c exampleapp --json
   ```
   
     로그인 하기 위한 값 toouse hello는 hello 서비스 사용자 이름에 나열 된 hello guid입니다.
   
   ```azurecli
   [
     {
       "objectId": "ff863613-e5e2-4a6b-af07-fff6f2de3f4e",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "7132aca4-1bdb-4238-ad81-996ff91d8db4",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "7132aca4-1bdb-4238-ad81-996ff91d8db4"
       ]
     }
   ]
   ```
3. Hello 서비스 사용자로 로그인 합니다.
   
   ```azurecli
   azure login -u 7132aca4-1bdb-4238-ad81-996ff91d8db4 --service-principal --tenant {tenant-id}
   ```
   
    Hello 암호를 묻는 메시지가 나타납니다. Hello AD 응용 프로그램을 만들 때 지정한 hello 암호를 제공 합니다.
   
   ```azurecli
   info:    Executing command login
   Password: ********
   ```

만든 hello 서비스 사용자에 대 한 hello 서비스 사용자로 인증 하는 이제 됩니다.

또는의 hello 명령줄 toolog에서 REST 작업을 호출할 수 있습니다. Hello 인증 응답에서 다른 작업과 함께 사용 하기 위해 hello 액세스 토큰을 검색할 수 있습니다. REST 작업을 호출 하 여 hello 액세스 토큰을 검색 하는 예제를 보려면 [액세스 토큰 생성](resource-manager-rest-api.md#generating-an-access-token)합니다.

## <a name="create-service-principal-with-certificate"></a>인증서를 사용하여 서비스 주체 만들기
이 섹션에서는 hello 단계를 수행할 수 있습니다.

* 자체 서명된 인증서 만들기
* hello 인증서 및 hello 서비스 사용자를 사용 하 여 hello AD 응용 프로그램 만들기
* hello 판독기 역할 toohello 서비스 사용자를 할당 합니다.

이 단계는 toocomplete, 있어야 [OpenSSL](http://www.openssl.org/) 설치 합니다.

1. 자체 서명된 인증서를 만듭니다.
   
   ```
   openssl req -x509 -days 3650 -newkey rsa:2048 -out cert.pem -nodes -subj '/CN=exampleapp'
   ```

2. 앞 단계 만든 두 개의 파일-privkey.pem 및 cert.pem 번호입니다. 단일 파일로 hello 공개 및 개인 키를 결합 합니다.

   ```
   cat privkey.pem cert.pem > examplecert.pem
   ```

3. 열기 hello **examplecert.pem** 파일를 찾아서 사이의 문자의 긴 시퀀스가 hello **---BEGIN 인증서---** 및 **---END 인증서---**합니다. Hello 인증서 데이터를 복사 합니다. Hello 서비스 사용자를 만들 때이 데이터를 매개 변수로 전달 합니다.

4. Tooyour 계정에 로그인 합니다.

   ```azurecli
   azure login
   ```
5. 다음 명령을 hello와 같이 hello 이름을 hello 응용 프로그램의 성능과 hello 인증서 데이터를 제공 하는 toocreate hello 서비스 사용자:
     
   ```azurecli
   azure ad sp create -n exampleapp --cert-value {certificate data}
   ```
     
   hello 새 서비스 사용자가 반환 됩니다. hello 개체 Id 사용 권한을 부여할 때 필요 합니다. 서비스 사용자 이름 hello로 나열 된 hello guid 로그인 할 때 필요 합니다. 이 guid는 hello hello 응용 프로그램 id와 동일한 값입니다. Hello 샘플 응용 프로그램에서이 값은 참조 tooas hello 클라이언트 id입니다. 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating service principal for application 4fd39843-c338-417d-b549-a545f584a74+
     data:    Object Id:        7dbc8265-51ed-4038-8e13-31948c7f4ce7
     data:    Display Name:     exampleapp
     data:    Service Principal Names:
     data:                      4fd39843-c338-417d-b549-a545f584a745
     data:                      https://www.contoso.org/example
     info:    ad sp create command OK
   ```
6. 구독에 대해 hello 서비스 보안 주체 권한을 부여 합니다. 이 예제에서는 권한을 tooread hello 구독에 있는 모든 리소스 수 있게 하는 hello 서비스 보안 주체 toohello Reader 역할에 추가 합니다. 다른 역할에 대해서는 [RBAC: 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md)을 참조하세요. Hello objectid 매개 변수에 대 한 hello hello 응용 프로그램을 만들 때 사용한 개체 Id를 제공 합니다. 이 명령은 실행 하기 전에 Azure Active Directory 전체 hello 제공 하는 서비스 새 주 toopropagate 약간의 시간이 허용 해야 합니다. 이러한 명령을 수동으로 실행할 때 작업 간에 충분 한 시간이 경과되었습니다. 스크립트에는 단계 toosleep hello 명령 사이 추가 해야 (같은 `sleep 15`). 보안 주체는 오류 상자가 hello hello 디렉터리에 존재 하지 않는 표시 되 면 hello 명령을 다시 실행 하십시오.
   
   ```azurecli
   azure role assignment create --objectId 7dbc8265-51ed-4038-8e13-31948c7f4ce7 -o Reader -c /subscriptions/{subscriptionId}/
   ```
  
### <a name="provide-certificate-through-automated-azure-cli-script"></a>자동화된 Azure CLI 스크립트를 통해 인증서 제공
이제, hello 응용 프로그램 tooperform 작업으로 toolog에 필요 합니다.

1. 서비스 사용자로 로그인 할 때마다 AD 앱에 대 한 hello 디렉터리의 tooprovide hello 테 넌 트 id가 필요 합니다. 테넌트는 Azure Active Directory의 인스턴스입니다. 현재 인증 된 구독을 사용 하 여에 대 한 tooretrieve hello 테 넌 트 id:
   
   ```azurecli
   azure account show
   ```
   
   반환하는 내용은 다음과 같습니다.
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
   Tooget hello 테 넌 트 id는 다른 구독 해야 할 경우 다음 명령을 hello를 사용 합니다.
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. tooretrieve hello 인증서 지문 및 필요 하지 않은 문자 제거를 따르십시오.
   
   ```
   openssl x509 -in "C:\certificates\examplecert.pem" -fingerprint -noout | sed 's/SHA1 Fingerprint=//g'  | sed 's/://g'
   ```
   
   다음과 유사한 지문 값을 반환합니다.
   
   ```
   30996D9CE48A0B6E0CD49DBB9A48059BF9355851
   ```
3. 로그인 하기 위한 tooretrieve hello 클라이언트 id toouse 해야 할 경우 사용 합니다.
   
   ```azurecli
   azure ad sp show -c exampleapp
   ```
   
   로그인 하기 위한 값 toouse hello는 hello 서비스 사용자 이름에 나열 된 hello guid입니다.
     
   ```azurecli
   [
     {
       "objectId": "7dbc8265-51ed-4038-8e13-31948c7f4ce7",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "4fd39843-c338-417d-b549-a545f584a745",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "4fd39843-c338-417d-b549-a545f584a745"
       ]
     }
   ]
   ```
4. Hello 서비스 사용자로 로그인 합니다.
   
   ```azurecli
   azure login --service-principal --tenant {tenant-id} -u 4fd39843-c338-417d-b549-a545f584a745 --certificate-file C:\certificates\examplecert.pem --thumbprint {thumbprint}
   ```

Hello 만든 Azure Active Directory 응용 프로그램에 대 한 hello 서비스 사용자로 인증 하는 이제 됩니다.

## <a name="change-credentials"></a>자격 증명 변경

보안 또는 자격 증명 만료 때문에 AD 응용 프로그램에 대 한 toochange hello 자격 증명 사용 `azure ad app set`합니다.

toochange 암호를 사용 합니다.

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --password p@ssword
```

toochange 인증서 값을 사용 합니다.

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --cert-value {certificate data}
```

## <a name="debug"></a>디버그

서비스 사용자를 만들 때 다음 오류 hello를 발생할 수 있습니다.

* **"Authentication_Unauthorized"** 또는 **"hello 컨텍스트에서 구독이 찾을 수 있습니다."** -이 오류가 나타나는 hello 사용자 계정에 없을 때 [필요한 권한](#required-permissions) hello Azure Active Directory tooregister 응용 프로그램에 있습니다. 일반적으로 Azure Active Directory의 관리 사용자만 앱을 등록할 수 있고 사용자 계정은 관리자가 아니면 이 오류가 표시됩니다. 관리자 tooeither tooenable 사용자 tooregister 응용 프로그램이 나 있습니다 tooan 관리자 역할 할당을 요청 합니다.

* 계정 **"동작이 되어 있지 않습니다 권한 부여 tooperform 'Microsoft.Authorization/roleAssignments/write' 범위 ' / 구독 / {guid}'에 대해."**  -계정에 없을 때 충분 한 사용 권한을 tooassign 역할 tooan id를이 오류를 참조 하십시오. 구독 관리자 tooadd 요청 tooUser 액세스 관리자에 게 역할입니다.

## <a name="sample-applications"></a>샘플 응용 프로그램
서로 다른 플랫폼을 통해 응용 프로그램 hello로 로그인 하는 방법에 대 한 정보를 보려면

* [.NET](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [Java](/java/azure/java-sdk-azure-authenticate)
* [Node.JS](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [Python](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [Ruby](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a>다음 단계
* 리소스 관리를 위해 Azure에 응용 프로그램을 통합 하는 기능에 대 한 자세한 내용은 참조 하십시오. [hello Azure 리소스 관리자 API가 있는 개발자 가이드 tooauthorization](resource-manager-api-authentication.md)합니다.
* tooget 인증서 및 Azure CLI를 사용 하는 방법에 대 한 자세한 내용은 참조 [Linux 명령줄에서 Azure 서비스 보안 주체와 인증서 기반 인증](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx)합니다. 
* 목록이 부여 하거나 거부 toousers 수 있는 작업에 대 한 참조 [Azure 리소스 관리자 리소스 공급자 작업](../active-directory/role-based-access-control-resource-provider-operations.md)합니다.
