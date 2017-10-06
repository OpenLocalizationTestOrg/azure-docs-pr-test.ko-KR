---
title: "Azure Blob 저장소 끝점에 대 한 사용자 지정 도메인 이름 aaaConfigure | Microsoft Docs"
description: "Azure 저장소 계정에 Azure 포털 toomap hello 사용자 고유의 정식 이름 (CNAME) toohello Blob 저장소 끝점을 사용 합니다."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: aaafd8c5-eacb-49dc-8c8b-3f7011ad5e92
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: marsma
ms.openlocfilehash: 6cca6a6e1dbb69e7078df7ed11b04e8b921ec2f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-custom-domain-name-for-your-blob-storage-endpoint"></a>Blob 저장소 끝점에 대한 사용자 지정 도메인 이름 구성

Azure 저장소 계정에서 Blob 데이터에 액세스할 수 있도록 사용자 지정 도메인을 구성할 수 있습니다. Blob 저장소에 대 한 기본 끝점을 hello `<storage-account-name>.blob.core.windows.net`합니다. 사용자 지정 도메인과 같은 하위 도메인을 매핑하는 경우 **www.contoso.com** toohello 저장소 계정의 blob 끝점, 사용자가 액세스할 수 blob 해당 도메인을 사용 하 여 저장소 계정에는 데이터입니다.

> [!IMPORTANT]
> Azure Storage는 아직 기본적으로 사용자 지정 도메인으로 HTTPS를 지원하지 않습니다. 현재 수 [hello Azure CDN tooaccess blob를 사용 하 여 HTTPS를 통해 사용자 지정 도메인과](./storage-https-custom-domain-cdn.md)합니다.
>

hello 다음 표에 나와 라는 저장소 계정에 있는 blob 데이터에 대 한 몇 가지 샘플 Url **mystorageaccount**합니다. 저장소 계정이 hello에 대 한 hello 사용자 지정 도메인 등록 **www.contoso.com**:

| 리소스 종류 | 기본 URL | 사용자 지정 도메인 URL |
| --- | --- | --- |
| 저장소 계정 | http://mystorageaccount.blob.core.windows.net | http://www.contoso.com |
| Blob |http://mystorageaccount.blob.core.windows.net/mycontainer/myblob | http://www.contoso.com/mycontainer/myblob |
| 루트 컨테이너 | http://mystorageaccount.blob.core.windows.net/myblob 또는 http://mystorageaccount.blob.core.windows.net/$root/myblob| http://www.contoso.com/myblob 또는 http://www.contoso.com/$root/myblob |

## <a name="direct-vs-intermediary-domain-mapping"></a>직접 도메인 매핑과 중간 도메인 매핑

두 가지 방법으로 toopoint 저장소 계정에 대 한 사용자 지정 도메인 toohello blob 끝점 가지: CNAME 매핑과 hello를 사용 하 여 직접 *asverify* 중간 하위 도메인입니다.

### <a name="direct-cname-mapping"></a>직접 CNAME 매핑

hello 첫 번째 및 가장 간단한 방법은 toocreate toohello blob 끝점을 직접 사용자 지정 도메인 및 하위 도메인을 매핑하는 정식 이름 (CNAME) 레코드입니다. CNAME 레코드는 원본 도메인 tooa 대상 도메인을 매핑하는 도메인 이름 (DNS) 시스템 기능입니다. 이 경우 hello 원본 도메인은 사용자 고유의 사용자 지정 도메인 및 하위 도메인, 예를 들어 *www.contoso.com*. hello 대상 도메인은 Blob 서비스 끝점, 예를 들어  *mystorageaccount.blob.core.windows.net*합니다.

hello 직접적인 방법에 대해서는 [사용자 지정 도메인 등록](#register-a-custom-domain)합니다.

### <a name="intermediary-mapping-with-asverify"></a>*asverify*를 사용하여 중간 매핑

두 번째 방법은 hello 또한 CNAME 레코드를 사용 하 여 하지만 Azure tooavoid 가동 중지 시간에서 인식 되는 특별 한 하위 도메인을 사용 하는 먼저: **asverify**합니다.

사용자 지정 도메인 tooa blob 끝점을 매핑하 hello 프로세스 hello에 등록 하는 동안 hello 도메인에 대 한 가동 중지 시간이 짧은 기간 동안 될 수 있습니다 [Azure 포털](https://portal.azure.com)합니다. 사용자 지정 도메인에서 현재 작동 중단 시간이 없는 필요로 하는 서비스 수준 계약 (SLA)으로 응용 프로그램을 지 원하는 경우 hello Azure를 사용할 수 있습니다 *asverify* 중간 등록 단계와 하위 도메인입니다. 중간 이렇게 하면 사용자 수 tooaccess 도메인 클래스 중는 hello DNS 매핑이 수행 됩니다.

hello 중간 메서드에 대해서는 [hello를 사용 하 여 사용자 지정 도메인 등록 *asverify* 하위 도메인](#register-a-custom-domain-using-the-asverify-subdomain)합니다.

## <a name="register-a-custom-domain"></a>사용자 지정 도메인 등록
없거나 현재 사용자 지정 도메인이 응용 프로그램을 호스팅하지 않는 tooyour 간단 하 게 사용할 수 없는 사용자가 되 고 hello 도메인에 대 한 문제 없이 경우이 절차 tooregister 사용자 지정 도메인을 사용 합니다.

현재 사용자 지정 도메인이 가동 중지 시간을 가질 수 없는 응용 프로그램을 지원 하 고, 경우에 설명 된 hello 절차에 따라 [hello를 사용 하 여 사용자 지정 도메인 등록 *asverify* 하위 도메인](#register-a-custom-domain-using-the-asverify-subdomain)합니다.

사용자 지정 도메인 이름을 tooconfigure 만들어야 새 CNAME 레코드를 DNS에 합니다. hello CNAME 레코드는 도메인 이름에 대 한 별칭을 지정합니다. 이 경우 저장소 계정에 대 한 사용자 지정 도메인 toohello Blob 저장소 끝점 주소가 hello를 매핑합니다.

일반적으로 도메인 등록 기관의 웹 사이트에서 도메인의 DNS 설정을 관리할 수 있습니다. 각 등록자 CNAME 레코드를 지정 하는 유사 하지만 약간 다른 방법은 갖지만 hello 개념 동일 hello 됩니다. 일부 기본 도메인 등록 패키지 제공 하지 않습니다 DNS 구성을 tooupgrade 수 있으므로 도메인 등록 패키지 hello CNAME 레코드를 만들 수 있습니다.

1. Hello에 tooyour 저장소 계정을 탐색 [Azure 포털](https://portal.azure.com)합니다.
1. 아래 **BLOB 서비스** hello 메뉴 블레이드에서 선택 **사용자 지정 도메인** tooopen hello *사용자 지정 도메인* 블레이드입니다.
1. Tooyour 도메인 등록 기관의 웹 사이트에서 오류를 로깅하고 toohello DNS 관리 페이지로 이동 합니다. **도메인 이름**, **DNS** 또는 **이름 서버 관리**와 같은 섹션에서 이를 찾을 수 있습니다.
1. CNAMEs를 관리 하기 위한 hello 섹션을 찾습니다. Toogo tooan 고급 설정 페이지를 hello 단어를 검색할 수도 있습니다 **CNAME**, **별칭**, 또는 **하위 도메인**합니다.
1. 새 CNAME 레코드를 만들어 **www** 또는 **photos**와 같은 하위 도메인 별칭을 지정합니다. 그런 다음 hello 형태로 표시 하 여 Blob 서비스 끝점 호스트 이름, 제공 **mystorageaccount.blob.core.windows.net** (여기서 *mystorageaccount* hello 저장소 계정의 이름입니다). hello의 항목 # 1에에서 표시 되는 hello 호스트 이름 toouse *사용자 지정 도메인* hello 블레이드 [Azure 포털](https://portal.azure.com)합니다.
1. Hello에 hello 텍스트 상자에서 *사용자 지정 도메인* hello 블레이드 [Azure 포털](https://portal.azure.com), hello hello 하위 도메인을 포함 하 여 사용자 지정 도메인 이름을 입력 합니다. 예를 들어 도메인이 **contoso.com**이고 하위 도메인 별칭이 **www**이면 **www.contoso.com**을 입력합니다. 하위 도메인 경우 **사진**, 입력 **photos.contoso.com**. hello 하위 도메인이 *필요한*합니다.
1. 선택 **저장** hello에 *사용자 지정 도메인* 블레이드 tooregister 사용자 지정 도메인입니다. Hello 등록에 성공 하면 저장소 계정의 성공적으로 업데이트 된 포털 알림이 표시 됩니다.

새 CNAME 레코드는 DNS를 통해 전파 된, 사용자가으로 hello 적절 한 사용 권한을 갖습니다 사용자 지정 도메인을 사용 하 여 blob 데이터를 볼 수 있습니다.

## <a name="register-a-custom-domain-using-hello-asverify-subdomain"></a>Hello를 사용 하 여 사용자 지정 도메인 등록 *asverify* 하위 도메인
이 절차 tooregister를 사용 하 여 사용자 지정 도메인 사용자 지정 도메인으로 SLA 요구 하는 응용 프로그램에서 현재 지 원하는 경우 가동 중지 시간 없이 수 있습니다. 로 가리키는 CNAME를 만들면 여 `asverify.<subdomain>.<customdomain>` 너무`asverify.<storageaccount>.blob.core.windows.net`, Azure 사용한 도메인을 미리 등록할 수 있습니다. 시작 하는 두 번째 CNAME를 만들 수 있습니다 `<subdomain>.<customdomain>` 너무`<storageaccount>.blob.core.windows.net`, 이때 트래픽 tooyour 사용자 지정 도메인 tooyour 방향이 지정 된 blob 끝점 됩니다.

hello **asverify** 하위 도메인은 Azure에서 인식 되는 특별 한 하위 도메인입니다. 앞에 추가 하 여 `asverify` tooyour 자체 하위 도메인을 허용 하면 Azure toorecognize 사용자 지정 도메인 hello 도메인에 대 한 hello DNS 레코드를 수정 하지 않고 있습니다. Hello 도메인에 대 한 hello DNS 레코드를 수정 수행 하면 중단 시간 없이 매핑된 toohello blob 끝점 됩니다.

1. Hello에 tooyour 저장소 계정을 탐색 [Azure 포털](https://portal.azure.com)합니다.
1. 아래 **BLOB 서비스** hello 메뉴 블레이드에서 선택 **사용자 지정 도메인** tooopen hello *사용자 지정 도메인* 블레이드입니다.
1. Tooyour DNS 공급자의 웹 사이트에서 오류를 로깅하고 toohello DNS 관리 페이지로 이동 합니다. **도메인 이름**, **DNS** 또는 **이름 서버 관리**와 같은 섹션에서 이를 찾을 수 있습니다.
1. CNAMEs를 관리 하기 위한 hello 섹션을 찾습니다. Toogo tooan 고급 설정 페이지를 hello 단어를 검색할 수도 있습니다 **CNAME**, **별칭**, 또는 **하위 도메인**합니다.
1. 새 CNAME 레코드를 만들고 hello를 포함 하는 하위 도메인 별칭을 제공 *asverify* 하위 도메인입니다. 예를 들어 **asverify.www** 또는 **asverify.photos**입니다. 그런 다음 hello 형태로 표시 하 여 Blob 서비스 끝점 호스트 이름, 제공 **asverify.mystorageaccount.blob.core.windows.net** (여기서 **mystorageaccount** hello 저장소 계정의 이름입니다). hello 호스트 이름 toouse hello의 항목 # 2에에서 표시 *사용자 지정 도메인* hello 블레이드 [Azure 포털](https://portal.azure.com)합니다.
1. Hello에 hello 텍스트 상자에서 *사용자 지정 도메인* hello 블레이드 [Azure 포털](https://portal.azure.com), hello hello 하위 도메인을 포함 하 여 사용자 지정 도메인 이름을 입력 합니다. *asverify*를 포함하지 않습니다. 예를 들어 도메인이 **contoso.com**이고 하위 도메인 별칭이 **www**이면 **www.contoso.com**을 입력합니다. 하위 도메인 경우 **사진**, 입력 **photos.contoso.com**. hello 하위 도메인이 필요 합니다.
1. 선택 hello **간접 CNAME 유효성 검사를 사용 하 여** 확인란을 선택 합니다.
1. 선택 **저장** hello에 *사용자 지정 도메인* 블레이드 tooregister 사용자 지정 도메인입니다. Hello 등록에 성공 하면 저장소 계정의 성공적으로 업데이트 했는지 한다는 포털 알림 메시지를 표시 됩니다. 이 시점에서 Azure에 의해 확인 된 사용자 지정 도메인 관리 되지만 트래픽 tooyour 도메인을 아직 라우팅이 tooyour 저장소 계정.
1. Tooyour DNS 공급자의 웹 사이트를 반환 하 고 하위 도메인 tooyour Blob 서비스 끝점을 매핑하는 다른 CNAME 레코드를 만듭니다. 예를 들어 hello 하위 도메인으로 지정 **www** 또는 **사진** (hello 없이 *asverify*), 호스트 이름으로 hello 및  **mystorageaccount.blob.core.windows.net** (여기서 **mystorageaccount** hello 저장소 계정의 이름입니다). 이 단계를 통해 사용자 지정 도메인의 hello 등록 완료 되었습니다.
1. 마지막으로, 포함 하는 hello 만든 hello CNAME 레코드를 삭제할 수 있습니다 **asverify** 하위 도메인으로이 중간 단계로 필요 합니다.

새 CNAME 레코드는 DNS를 통해 전파 된, 사용자가으로 hello 적절 한 사용 권한을 갖습니다 사용자 지정 도메인을 사용 하 여 blob 데이터를 볼 수 있습니다.

## <a name="test-your-custom-domain"></a>사용자 지정 도메인 테스트

사용자 지정 도메인은 tooconfirm tooyour Blob 서비스 끝점을 실제로 매핑된, 저장소 계정 내에서 공용 컨테이너에서 blob을 만듭니다. 그런 다음 웹 브라우저에서 hello 형식 tooaccess hello blob 뒤에 URI을 사용 합니다.

`http://<subdomain.customdomain>/<mycontainer>/<myblob>`

예를 들어 다음 URI tooaccess hello에서 web form hello를 사용할 수 있습니다 **myforms** 컨테이너에서 hello **photos.contoso.com** 사용자 지정 하위 도메인:

`http://photos.contoso.com/myforms/applicationform.htm`

## <a name="deregister-a-custom-domain"></a>사용자 지정 도메인 등록 취소

Blob 저장소 끝점에 대 한 사용자 지정 도메인 tooderegister 다음 절차를 수행 하는 hello 중 하나를 사용 합니다.

### <a name="azure-portal"></a>Azure portal

Hello Azure 포털 tooremove hello 사용자 지정 도메인 설정에 hello 다음을 수행 합니다.

1. Hello에 tooyour 저장소 계정을 탐색 [Azure 포털](https://portal.azure.com)합니다.
1. 아래 **BLOB 서비스** hello 메뉴 블레이드에서 선택 **사용자 지정 도메인** tooopen hello *사용자 지정 도메인* 블레이드입니다.
1. 사용자 지정 도메인 이름을 포함 하는 hello 텍스트 상자의 선택을 취소 hello 내용입니다.
1. 선택 hello **저장** 단추입니다.

사용자 지정 도메인 hello 성공적으로 제거 되 면 저장소 계정을 성공적으로 업데이트 했는지 한다는 포털 알림 메시지를 표시 됩니다.

### <a name="azure-cli-20"></a>Azure CLI 2.0

사용 하 여 hello [az 저장소 계정 업데이트](https://docs.microsoft.com/cli/azure/storage/account#update) CLI 명령 및 빈 문자열을 지정 (`""`) hello에 대 한 `--custom-domain` 인수 값 tooremove 사용자 지정 도메인 등록 합니다.

* 명령 형식:

  ```azurecli
  az storage account update \
      --name <storage-account-name> \
      --resource-group <resource-group-name> \
      --custom-domain ""
  ```

* 명령 예:

  ```azurecli
  az storage account update \
      --name mystorageaccount \
      --resource-group myresourcegroup \
      --custom-domain ""
  ```

### <a name="powershell"></a>PowerShell

사용 하 여 hello [집합 AzureRmStorageAccount](/powershell/module/azurerm.storage/set-azurermstorageaccount) PowerShell cmdlet 빈 문자열을 지정 하 고 (`""`) hello에 대 한 `-CustomDomainName` 인수 값 tooremove 사용자 지정 도메인 등록 합니다.

* 명령 형식:

  ```powershell
  Set-AzureRmStorageAccount `
      -ResourceGroupName "<resource-group-name>" `
      -AccountName "<storage-account-name>" `
      -CustomDomainName ""
  ```

* 명령 예:

  ```powershell
  Set-AzureRmStorageAccount `
      -ResourceGroupName "myresourcegroup" `
      -AccountName "mystorageaccount" `
      -CustomDomainName ""
  ```

## <a name="next-steps"></a>다음 단계
* [사용자 지정 도메인 tooan Azure 콘텐츠 배달 네트워크 (CDN) 끝점 매핑](../cdn/cdn-map-content-to-custom-domain.md)
* [HTTPS를 통해 사용자 지정 도메인에서 hello Azure CDN tooaccess blob 사용](./storage-https-custom-domain-cdn.md)
