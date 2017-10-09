---
title: "aaaViewing 호스트 이름이 수정 | Microsoft Docs"
description: "Azure 가상 컴퓨터에 대 한 tooview 및 변경 hostnames 웹 방식 및 이름 확인에 대 한 작업자 역할"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c668cd8e-4e43-4d05-acc3-db64fa78d828
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.openlocfilehash: 17d0dd7911754a94db3f37b924b4687da1c70aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="viewing-and-modifying-hostnames"></a>호스트 이름 보기 및 수정
호스트 이름으로 참조 되는 역할 인스턴스 toobe tooallow, 각 역할에 대 한 hello 서비스 구성 파일에서 hello 호스트 이름에 대 한 hello 값을 설정 해야 합니다. Hello 필요한 호스트 이름 toohello를 추가 하 여 그렇게 **vmName** hello 특성 **역할** 요소입니다. 값의 hello hello **vmName** 특성은 각 역할 인스턴스의 호스트 이름 hello에 대 한 기준으로 사용 합니다. 예를 들어 경우 **vmName** 은 *webrole* 해당 역할의 인스턴스가 hello 인스턴스의 호스트 이름을 hello 됩니다 *webrole0*, *webrole1* , 및 *webrole2*합니다. 가상 컴퓨터에 대 한 호스트 이름을 hello hello 가상 컴퓨터 이름에 따라 채워집니다. 때문에 toospecify hello 구성 파일에서 가상 컴퓨터에 대 한 호스트 이름을 않아도 됩니다. Microsoft Azure 서비스 구성에 대한 자세한 내용은 [Azure 서비스 구성 스키마(.cscfg 파일)](https://msdn.microsoft.com/library/azure/ee758710.aspx)

## <a name="viewing-hostnames"></a>호스트 이름 보기
아래의 hello 도구 중 하나를 사용 하 여 클라우드 서비스에서 가상 컴퓨터와 역할 인스턴스 hello 호스트 이름을 볼 수 있습니다.

### <a name="azure-portal"></a>Azure 포털
Hello를 사용할 수 있습니다 [Azure 포털](http://portal.azure.com) hello 개요 블레이드에 가상 컴퓨터에 가상 컴퓨터에 대 한 tooview hello 호스트 이름입니다. 에 대 한 값을 표시 하는 hello 블레이드 있음을 명심 **이름** 및 **호스트 이름**합니다. Hello 호스트 이름 변경 동일 hello 처음 경우도 있지만 hello hello 가상 컴퓨터나 역할 인스턴스 이름을 변경 되지 않습니다.

Hello Azure 포털에서에서 역할 인스턴스를 볼 수도 있습니다 하지만 클라우드 서비스의 hello 인스턴스를 나열 하는 경우 hello 호스트 이름이 표시 되지 않습니다. 각 인스턴스의 이름을 표시 하지만 해당 이름 hello 호스트 이름을 표시 하지 않습니다.

### <a name="service-configuration-file"></a>서비스 구성 파일
Hello에서 배포 된 서비스에 대 한 hello 서비스 구성 파일을 다운로드할 수 있습니다 **구성** 블레이드 hello Azure 포털의에서 hello 서비스입니다. Hello에 대 한 확인할 수 있습니다 **vmName** hello에 대 한 특성 **역할 이름** 요소 toosee hello 호스트 이름입니다. 각 역할 인스턴스의 호스트 이름 hello에 대 한이 호스트 이름은 기본으로 사용 됩니다 염두에서에 둬야 합니다. 예를 들어 경우 **vmName** 은 *webrole* 해당 역할의 인스턴스가 hello 인스턴스의 호스트 이름을 hello 됩니다 *webrole0*, *webrole1* , 및 *webrole2*합니다.

### <a name="remote-desktop"></a>원격 데스크톱
원격 데스크톱 (Windows), Windows PowerShell 원격 (Windows) 또는 SSH (Linux / Windows) 연결 tooyour 가상 컴퓨터나 역할 인스턴스를 활성화 한 후에 다양 한 방법으로 활성 원격 데스크톱 연결에서 hello 호스트 이름을 볼 수 있습니다.

* Hello 명령 프롬프트 또는 SSH 터미널에 호스트 이름을 입력 합니다.
* Ipconfig를 입력/hello 명령에 모든 메시지 (Windows에만 해당)를 표시 합니다.
* Hello 시스템 뷰 hello 컴퓨터 이름 설정 (Windows에만 해당).

### <a name="azure-service-management-rest-api"></a>Azure 서비스 관리 REST API
REST 클라이언트에서 다음 지침을 따릅니다.

1. Azure 포털 클라이언트 인증서 tooconnect toohello 가졌는지 확인 합니다. 에 제공 된 hello 단계를 수행 하는 클라이언트 인증서를 tooobtain [하는 방법: 다운로드 및 게시 설정 가져오기 및 구독 정보](https://msdn.microsoft.com/library/dn385850.aspx)합니다. 
2. 값이 2013-11-01인 x-ms-version 헤더 항목을 설정합니다.
3. 형식에 따라 hello에 요청을 보내고: https://management.core.windows.net/\<subscrition id\>/서비스/hostedservices/\<서비스 이름\>? 포함 세부 = true
4. Hello에 대 한 확인 **HostName** 요소 각각에 대해 **RoleInstance** 요소입니다.

> [!WARNING]
> Hello를 확인 하 여 hello REST 호출 응답에서에서 클라우드 서비스에 대 한 hello 내부 도메인 접미사를 볼 수도 있습니다 **InternalDnsSuffix** 요소인 ipconfig를 실행 하 여/모두 (Windows), 원격 데스크톱 세션에서 명령 프롬프트에서에서 또는 또는 SSH 터미널 (Linux)에서 실행 중인 cat /etc/resolv.conf 합니다.
> 
> 

## <a name="modifying-a-hostname"></a>호스트 이름 수정
수정 된 서비스 구성 파일을 업로드 하거나 원격 데스크톱 세션에서 hello 컴퓨터 바꾸면 역할 인스턴스 또는 가상 컴퓨터에 대 한 hello 호스트 이름을 수정할 수 있습니다.

## <a name="next-steps"></a>다음 단계
[이름 확인(DNS)](virtual-networks-name-resolution-for-vms-and-role-instances.md)

[Azure 서비스 구성 스키마(.cscfg)](https://msdn.microsoft.com/library/windowsazure/ee758710.aspx)

[Azure 가상 네트워크 구성 스키마](http://go.microsoft.com/fwlink/?LinkId=248093)

[네트워크 구성 파일을 사용하여 DNS 설정 지정](virtual-networks-specifying-a-dns-settings-in-a-virtual-network-configuration-file.md)

