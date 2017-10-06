---
title: "파일 tooAzure Azure CLI 1.0을 사용 하 여 DNS aaaImport와 내보내기 도메인 영역 | Microsoft Docs"
description: "어떻게 tooimport 및 내보내기는 DNS 영역 파일 tooAzure DNS Azure CLI 1.0을 사용 하 여 알아봅니다"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: f5797782-3005-4663-a488-ac0089809010
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 4c3163395e151e9934c730349b828c612491016f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-a-dns-zone-file-using-hello-azure-cli-10"></a>Hello Azure CLI 1.0을 사용 하 여 DNS 영역 파일 가져오기 및 내보내기 

이 문서 tooimport 및 내보내기 DNS 영역 파일을 Azure DNS를 사용 하 여 Azure CLI 1.0 hello 하는 방법을 안내 합니다.

## <a name="introduction-toodns-zone-migration"></a>소개 tooDNS 영역 마이그레이션

DNS 영역 파일은 hello 영역의 모든 이름을 DNS (도메인) 레코드의 세부 정보가 포함 된 텍스트 파일. 표준 형식을 따르며 이는 DNS 시스템 간에 DNS 레코드를 전송하는 데 적합하도록 만듭니다. 영역 파일을 사용 하 여 며 빠른, 신뢰할 수 있는 편리한 방법 tootransfer DNS 영역 내부 또는 외부로 Azure DNS 합니다.

Azure DNS 파일 가져오기 및 내보내기 영역 hello Azure CLI (명령줄 인터페이스)를 사용 하 여 지원 합니다. 영역 파일 가져오기는 **하지** hello Azure 포털 또는 Azure PowerShell을 통해 현재 지원 합니다.

hello Azure CLI 1.0은 Azure 서비스 관리에 사용 되는 플랫폼 간 명령줄 도구입니다. Hello에서 hello Windows, Mac 및 Linux 플랫폼에 사용할 수 [Azure 다운로드 페이지](https://azure.microsoft.com/downloads/)합니다. 가져오기 및 영역 파일을 내보내는 hello 가장 일반적인 이름 서버 소프트웨어에 대 한 플랫폼 간 지원 반드시 [바인딩할](https://www.isc.org/downloads/bind/), 일반적으로 Linux에서 실행 합니다.

> [!NOTE]
> 현재 hello Azure CLI의 버전은 합니다. CLI1.0은 Node.js를 기반으로 하며 "azure"로 시작하는 명령이 있습니다.
> CLI2.0은 Python을 기반으로 하며 "az"로 시작하는 명령이 있습니다. 영역 파일 가져오기는 두 버전에서에서 지원 되지만, 권장 hello CLI1.0 명령을 사용 하 여이 페이지에 설명 된 대로 합니다.

## <a name="obtain-your-existing-dns-zone-file"></a>기존 DNS 영역 파일 가져오기

Azure DNS로 DNS 영역 파일을 가져오기 전에 tooobtain hello 영역 파일의 복사본을 해야 합니다. 이 파일의 원본을 hello hello DNS 영역이 현재 호스트 된 위치에 따라 다릅니다.

* DNS 영역에는 파트너 서비스 (예: 도메인 등록자, 전용된 DNS 호스팅 공급자 또는 다른 클라우드 공급자)에서 호스트 될 경우 해당 서비스 hello 기능 toodownload hello DNS 영역 파일을 제공 해야 합니다.
* Hello 영역 파일에 대 한 hello 기본 폴더는 DNS 영역이 Windows DNS에 호스트 될 경우 **%systemroot%\system32\dns**합니다. hello 전체 경로 tooeach 영역 파일 hello에도 표시 **일반** hello DNS 콘솔의 탭 합니다.
* 각 영역에 대 한 hello 영역 파일의 hello 위치 hello 바인딩 구성 파일에 지정 된 DNS 영역이 BIND를 사용 하 여 호스팅되 경우 **named.conf**합니다.

> [!NOTE]
> GoDaddy에서 다운로드한 영역 파일은 약간 비표준 형식을 가지고 있습니다. 필요한 toocorrect이 Azure DNS로 이러한 영역 파일을 가져오기 전에 합니다.
>
> 각 DNS 레코드의 RDATA hello에 대 한 DNS 이름을 정규화 된 이름으로 지정 되어 있지만 종료 없는 경우 "." 즉, 이 이름은 다른 DNS 시스템에서 상대 이름으로 해석됩니다. Tooedit hello 영역 파일 tooappend hello 종료 해야 "." tootheir Azure DNS로 가져오기 전에 이름을 지정 합니다.
>
> CNAME 레코드 "www 3600 CNAME contoso.com에서" hello 너무 하 여 변경 해야 예를 들어 "www 3600 IN CNAME contoso.com"
> (끝에 "."가 있어야 함).

## <a name="import-a-dns-zone-file-into-azure-dns"></a>Azure DNS에 DNS 영역 파일 가져오기

영역이 아직 없는 경우 영역 파일을 가져오면 Azure DNS에서 새 영역을 만듭니다. Hello 영역에 이미 있으면 hello 레코드 집합 hello 영역 파일에 병합 해야 hello 기존 레코드 집합입니다.

### <a name="merge-behavior"></a>병합 동작

* 기존 및 새 레코드 집합은 기본적으로 병합됩니다. 병합된 레코드 집합 내의 동일한 레코드는 중복을 제거합니다.
* Hello를 지정 하 여 또는 `--force` 옵션, 가져오기 프로세스 대신 새 레코드 집합으로 설정 하는 기존 레코드 hello 합니다. 해당 레코드가 hello 가져온된 영역 파일에 설정 하지 않은 기존 레코드 집합 제거 되지 않습니다.
* 레코드 집합을 병합 될 때는 hello toolive TTL (time)의 기존 레코드 집합 사용 됩니다. 때 `--force` 는 사용 하는 hello hello 새 레코드 집합의 TTL 사용 됩니다.
* SOA () 매개 변수는 시작 (제외 하 고 `host`) hello 가져온된 영역 파일에 있는 여부에 관계 없이 항상 취해집니다 `--force` 사용 됩니다. 마찬가지로, hello 이름 서버 레코드 hello 영역 루트에서 설정에 대 한 hello TTL은 항상 파일에서 가져온 hello 가져온된 영역입니다.
* 기존 CNAME 가져온된 CNAME 레코드를 대체 하지 않습니다 hello 하지 않는 한 이름과 같은 이름을 hello를 사용 하 여 기록 `--force` 매개 변수를 지정 합니다.
* CNAME 레코드가 다른 레코드 사이 충돌이 발생 하는 경우 hello 다르지만 이름과 같은 이름을 입력 (하는 기존에 관계 없이 또는 새), hello 기존 레코드 유지 됩니다. 이 별개의 hello 사용 `--force`합니다.

### <a name="additional-information-about-importing"></a>가져오기에 대한 추가 정보

hello 다음 참고 사항에서는 hello 영역에 대 한 추가 기술 세부 정보 가져오기 프로세스입니다.

* hello `$TTL` 지시문은 선택적 이며 지원 됩니다. No `$TTL` 지시문이 주어진 경우 명시적 TTL 없는 레코드를 가져오는 tooa 기본 TTL 3600 (초)을 설정 합니다. 에 두 개를 기록 하는 경우 hello 동일한 레코드 집합이 지정 다른 TTLs, hello 더 낮은 값이 사용 됩니다.
* hello `$ORIGIN` 지시문은 선택적 이며 지원 됩니다. No `$ORIGIN` 설정 되 면 hello 기본 사용 되는 값은 hello 명령줄에 지정 된 대로 hello 영역 이름 (hello 종료 및 ".").
* hello `$INCLUDE` 및 `$GENERATE` 지시문이 지원 되지 않습니다.
* A, AAAA, CNAME, MX, NS, SOA, SRV, TXT 등의 레코드 형식을 지원합니다.
* hello SOA 레코드는 영역을 만들면 Azure DNS에서 자동으로 생성 됩니다. 모든 SOA 매개 변수는 hello 영역 파일에서 가져온 영역 파일을 가져올 때 *제외 하 고* hello `host` 매개 변수입니다. 이 매개 변수는 Azure DNS에서 제공 하는 hello 값을 사용 합니다. 즉,이 매개 변수는 toohello 기본 이름 서버가 Azure DNS를 제공한 참조 해야 합니다.
* hello 영역 루트에서 설정 하는 hello 이름 서버 레코드가 만들어집니다 자동으로 Azure DNS에서 hello 영역을 만들 때. 만 hello TTL이 레코드 집합을 가져옵니다. 이러한 레코드에는 Azure DNS에서 제공 하는 hello 이름 서버 이름이 포함 됩니다. 데이터를 기록 하는 hello hello 가져온된 영역 파일에 포함 된 hello 값으로 덮어쓰지 않습니다.
* 공개 미리 보기 중에 Azure DNS는 단일 문자 TXT 레코드만 지원합니다. 다중 문자열 TXT 레코드는 연결 및 잘린 too255 자가 하 여야 합니다.

### <a name="cli-format-and-values"></a>CLI 형식 및 값

hello hello Azure CLI 명령 tooimport DNS 영역의 형식은 다음과 같습니다.

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

값

* `<resource group>`hello Azure dns에서 영역 hello에 대 한 hello 리소스 그룹 이름이입니다.
* `<zone name>`hello hello 영역 이름이입니다.
* `<zone file name>`가져온 hello 영역 파일 toobe hello 경로/이름입니다.

이 이름 사용 하 여 영역 hello 리소스 그룹에 없는 경우 사용자에 대 한 생성 됩니다. Hello 영역에 이미 있으면 hello 가져온된 레코드 집합이 병합 됩니다 기존 레코드 집합. toooverwrite hello 기존 레코드 집합을 사용 하 여 hello `--force` 옵션입니다.

실제로 가져오지 않고을 사용 하 여 hello 영역 파일의 tooverify hello 형식을 `--parse-only` 옵션입니다.

### <a name="step-1-import-a-zone-file"></a>1단계. 영역 파일 가져오기

tooimport hello 영역에 대 한 영역 파일 **contoso.com**합니다.

1. Hello Azure CLI 1.0을 사용 하 여 Azure 구독 tooyour에 로그인 합니다.

    ```azurecli
    azure login
    ```

2. 저장할 toocreate 새 DNS 영역이 hello 구독을 선택 합니다.

    ```azurecli
    azure account set <subscription name>
    ```

3. Azure DNS는 Azure 리소스 관리자 전용 서비스 이므로 hello Azure CLI tooResource 전환 된 관리자 모드 여야 합니다.

    ```azurecli
    azure config mode arm
    ```

4. Hello Azure DNS 서비스를 사용 하기 전에 구독 toouse hello Microsoft.Network 리소스 공급자를 등록 해야 합니다. (이 작업은 각 구독에 대해 한 번만 수행하면 됩니다.)

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. 없는 경우 하나 이미, toocreate 리소스 관리자 리소스 그룹이 있어야 합니다.

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. tooimport hello 영역 **contoso.com** hello 파일에서 **contoso.com.txt** hello 리소스 그룹에 새 DNS 영역으로 **myresourcegroup**, hello 명령을 실행`azure network dns zone import`.<BR>이 명령은 hello 영역 파일을 로드 하 고 구문 분석 합니다. hello 명령 hello Azure DNS 서비스 toocreate hello 영역에는 일련의 명령 실행 하 고 hello 영역에서 모든 hello 레코드 집합 키를 누릅니다. hello 명령 오류 또는 경고와 함께 hello 콘솔 창에서 진행률을 보고합니다. 레코드 집합 계열에서 만들어지므로 큰 영역 파일을 몇 분 tooimport 걸릴 수 있습니다.

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-hello-zone"></a>2단계. Hello 영역 확인

tooverify hello DNS 영역 hello 파일을 가져온 후 hello 메서드를 다음 중 하나를 사용할 수 있습니다.

* 다음 Azure CLI 명령을 hello를 사용 하 여 hello 레코드를 나열할 수 있습니다.

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* Hello PowerShell cmdlet을 사용 하 여 hello 레코드를 나열할 수 있습니다 `Get-AzureRmDnsRecordSet`합니다.
* 사용할 수 있습니다 `nslookup` hello 레코드에 대 한 tooverify 이름 확인 합니다. Hello 영역을 아직 위임 되지 않습니다, 때문에 toospecify hello 올바른 Azure DNS 이름 서버에 명시적으로 필요 합니다. hello 다음 샘플에서는 tooretrieve hello 이름 서버 이름이 toohello 영역을 할당 하는 방식 IT tooquery hello "www"를 사용 하 여 기록 하는 방법을 보여 줍니다 `nslookup`합니다.

        C:\>azure network dns record-set show myresourcegroup contoso.com @ NS
        info:Executing command network dns record-set show
        + Looking up hello DNS Record Set "@" of type "NS"
        data:Id: /subscriptions/.../resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com/NS/@
        data:Name: @
        data:Type: Microsoft.Network/dnszones/NS
        data:Location: global
        data:TTL : 3600
        data:NS records
        data:Name server domain name : ns1-01.azure-dns.com
        data:Name server domain name : ns2-01.azure-dns.net
        data:Name server domain name : ns3-01.azure-dns.org
        data:Name server domain name : ns4-01.azure-dns.info
        data:
        info:network dns record-set show command OK

        C:\> nslookup www.contoso.com ns1-01.azure-dns.com

        Server: ns1-01.azure-dns.com
        Address:  40.90.4.1

        Name:www.contoso.com
        Addresses:  134.170.185.46
        134.170.188.221

### <a name="step-3-update-dns-delegation"></a>3단계. DNS 위임 업데이트

Hello 영역 올바로 가져왔는지, tooupdate hello DNS 위임 toopoint toohello 필요한 확인 한 후 Azure DNS 서버 이름을 지정 합니다. 자세한 내용은 hello 문서 참조 [hello DNS 위임 업데이트](dns-domain-delegation.md)합니다.

## <a name="export-a-dns-zone-file-from-azure-dns"></a>Azure DNS에서 DNS 영역 파일 내보내기

hello hello Azure CLI 명령 tooimport DNS 영역의 형식은 다음과 같습니다.

```azurecli
azure network dns zone export [options] <resource group> <zone name> <zone file name>
```

값

* `<resource group>`hello Azure dns에서 영역 hello에 대 한 hello 리소스 그룹 이름이입니다.
* `<zone name>`hello hello 영역 이름이입니다.
* `<zone file name>`내보낸 hello 영역 파일 toobe hello 경로/이름입니다.

Hello 영역 가져오기를 사용 하 여 먼저 toosign에 필요한, 구독을 선택 하 고 hello Azure CLI toouse Resource Manager 모드를 구성 합니다.

### <a name="tooexport-a-zone-file"></a>tooexport 영역 파일

1. Hello Azure CLI를 사용 하 여 Azure 구독 tooyour에 로그인 합니다.

    ```azurecli
    azure login
    ```

2. Hello 구독 저장할 toocreate DNS 영역을 선택 합니다.

    ```azurecli
    azure account set <subscription name>
    ```

3. Azure DNS는 Azure 리소스 관리자 전용 서비스입니다. hello Azure CLI tooResource 전환 된 관리자 모드 여야 합니다.

    ```azurecli
    azure config mode arm
    ```

4. tooexport hello 기존 Azure DNS 영역 **contoso.com** 리소스 그룹에 **myresourcegroup** toohello 파일 **contoso.com.txt** (hello 현재 폴더)을 실행 `azure network dns zone export`. 호출 hello Azure DNS 서비스 tooenumerate이이 명령은 hello 영역에서 레코드 집합 및 hello 결과 tooa 바인딩 호환 영역 파일을 내보냅니다.

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
