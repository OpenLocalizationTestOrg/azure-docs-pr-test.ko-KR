---
title: "웹 앱에 대 한 사용자 지정 DNS 레코드 aaaCreate | Microsoft Docs"
description: "어떻게 toocreate 사용자 지정 도메인 DNS Azure DNS를 사용 하 여 웹 앱에 대 한 기록 합니다."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 6c16608c-4819-44e7-ab88-306cf4d6efe5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 070c808a55bab922eb624d99ae5c275d8eaa5aaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a>사용자 지정 도메인에서 웹앱에 대한 DNS 레코드 만들기

웹 앱에 대 한 Azure DNS toohost 사용자 지정 도메인을 사용할 수 있습니다. 예를 들어 Azure 웹 앱을 만드는 하 고 사용자가 tooaccess 하려는 하거나 하 여 www.contoso.com 또는 contoso.com을 사용 하 여 FQDN으로 합니다.

toodo이 toocreate 두 레코드가:

* "A" 루트 레코드 포인팅 toocontoso.com
* "CNAME" toohello 가리키는 hello www 이름에 대 한 기록 레코드

Azure에서 웹 앱에 대 한 A 레코드를 만든 경우 레코드를 수동으로 업데이트 해야 하는 hello hello 웹 응용 프로그램은 변경에 대 한 기본 IP 주소를 hello 염두에서에 둬야 합니다.

## <a name="before-you-begin"></a>시작하기 전에

시작 하기 전에 먼저 Azure DNS에서 DNS 영역을 생성 하며 hello 영역 프로그램 등록자 tooAzure DNS에에서 위임 합니다.

1. toocreate DNS 영역에서 다음과 같이 hello [DNS 영역을 만드는](dns-getstarted-create-dnszone.md)합니다.
2. toodelegate 프로그램 DNS tooAzure DNS에서 다음과 같이 hello [DNS 도메인 위임](dns-domain-delegation.md)합니다.

영역을 만드는 tooAzure DNS 위임 후, 사용자 지정 도메인에 대 한 다음 레코드를 만들 수 있습니다.

## <a name="1-create-an-a-record-for-your-custom-domain"></a>1. 사용자 지정 도메인에 대한 A 레코드 만들기

A 레코드에 사용 되는 toomap 이름 tooits IP 주소입니다. 다음 예제는 hello에 A 레코드 tooan IPv4 주소와 할당 됩니다.

### <a name="step-1"></a>1단계

A 레코드를 만들고 변수 $rs tooa 할당

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a>2단계

Hello IPv4 값 이전에 만든 toohello 레코드 집합을 추가 합니다. "@" hello $rs 변수 할당을 사용 하 여 합니다. 할당 된 IPv4 값 hello 웹 앱에 대 한 IP 주소 hello 됩니다.

웹 앱에 대 한 toofind hello IP 주소에서 다음과 같이 hello [Azure 앱 서비스에서 사용자 지정 도메인 이름을 구성](../app-service-web/app-service-web-tutorial-custom-domain.md)합니다.

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a>3단계

Hello 변경 toohello 레코드 집합을 커밋하십시오. 사용 하 여 `Set-AzureRMDnsRecordSet` tooupload hello toohello 레코드 집합 tooAzure DNS를 변경 합니다.

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a>2. 사용자 지정 도메인에 대한 CNAME 레코드 만들기

도메인이 Azure DNS에서 이미 관리 되는 경우 (참조 [DNS 도메인 위임](dns-domain-delegation.md), hello 예제 toocreate contoso.azurewebsites.net에 대 한 CNAME 레코드를 따라 hello를 사용할 수 있습니다.

### <a name="step-1"></a>1단계

PowerShell를 열고 새 CNAME 레코드 집합을 만든 tooa 변수 $rs 할당 합니다. 이 예제에서는 "시간의 toolive" 600 초 DNS 영역에 "contoso.com" 이라는 CNAME 레코드 집합 형식을 만듭니다.

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

다음 예제는 hello hello 응답입니다.

```
Name              : www
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a>2단계

Hello CNAME 레코드 집합을 만든 후 toocreate toohello 웹 앱에 가리키는 별칭 값 필요.

이전에 "$rs" 변수를 할당 하는 hello를 사용 하 여 웹 응용 프로그램 contoso.azurewebsites.net hello에 대 한 toocreate hello 별칭 아래 hello PowerShell 명령을 사용할 수 있습니다.

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

다음 예제는 hello hello 응답입니다.

```
    Name              : www
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a>3단계

Hello를 사용 하 여 hello 변경 내용 커밋 `Set-AzureRMDnsRecordSet` cmdlet:

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

유효성을 검사할 수 hello 레코드가 올바르게 아래와 같이 hello "www.contoso.com" nslookup을 사용 하 여 쿼리를 통해 만들어진:

```
PS C:\> nslookup
Default Server:  Default
Address:  192.168.0.1

> www.contoso.com
Server:  default server
Address:  192.168.0.1

Non-authoritative answer:
Name:    <instance of web app service>.cloudapp.net
Address:  <ip of web app service>
Aliases:  www.contoso.com
contoso.azurewebsites.net
<instance of web app service>.vip.azurewebsites.windows.net
```

## <a name="create-an-awverify-record-for-web-apps"></a>웹앱에 대한 "awverify" 레코드 만들기

웹 앱에 대 한 toouse A 레코드를 결정 한 경우 있습니다 거쳐야 확인 프로세스 tooensure 있습니다 hello 고유의 사용자 지정 도메인입니다. 이 검증 단계는 "awverify"라는 특수 CNAME 레코드를 만들어 수행됩니다. 이 섹션에는 tooA 레코드에만 적용 됩니다.

### <a name="step-1"></a>1단계

Hello "awverify" 레코드를 만듭니다. Hello 아래의 예제에서는 사용자 지정 도메인 hello에 대 한 contoso.com tooverify 소유권에 대 한 hello "aweverify" 레코드를 만듭니다.

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

다음 예제는 hello hello 응답입니다.

```
Name              : awverify
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a>2단계

"Awverify" hello 레코드 집합을 만든 후 별칭 설정 hello CNAME 레코드를 할당 합니다. Hello 아래 예제에서는 우리는 hello CNAMe 레코드 집합 별칭 tooawverify.contoso.azurewebsites.net을 할당 합니다.

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

다음 예제는 hello hello 응답입니다.

```
    Name              : awverify
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {awverify.contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a>3단계

Hello를 사용 하 여 hello 변경 내용 커밋 `Set-AzureRMDnsRecordSet cmdlet`hello 명령 아래에 표시 된 것 처럼 합니다.

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a>다음 단계

Hello 단계에 따라 [응용 프로그램 서비스에 대 한 사용자 지정 도메인 이름 구성](../app-service-web/web-sites-custom-domain-name.md) tooconfigure 웹 앱 toouse 사용자 지정 도메인입니다.
