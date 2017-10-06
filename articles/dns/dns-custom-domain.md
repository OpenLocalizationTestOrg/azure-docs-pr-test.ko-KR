---
title: "Azure 리소스와 Azure DNS aaaIntegrate | Microsoft Docs"
description: "자세한 방법을 따라 Azure 리소스에 대 한 DNS tooprovide toouse Azure DNS 합니다."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: b9b6f829513f0ad9da510190c75bc60dc7431545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-dns-tooprovide-custom-domain-settings-for-an-azure-service"></a>Azure 서비스에 대 한 Azure DNS tooprovide 사용자 지정 도메인 설정 사용

Azure DNS는 사용자 지정 도메인을 지원하거나 FQDN(정규화된 도메인 이름)이 있는 모든 Azure 리소스에 대해 사용자 지정 도메인용 DNS를 제공합니다. 예제 Azure 웹 앱이 있는 사용자가 사용자 tooaccess 하거나 하 여 contoso.com 또는 www.contoso.com을 사용 하 여 FQDN으로 합니다. 이 문서에서는 사용자 지정 도메인을 사용하기 위해 Azure DNS로 Azure 서비스를 구성하는 과정을 안내합니다.

## <a name="prerequisites"></a>필수 조건

사용자 지정 도메인에 대 한 순서 toouse Azure DNS를 먼저 사용자 도메인 tooAzure DNS 위임 해야 합니다. 방문 [도메인 tooAzure DNS 위임](./dns-delegate-domain-azure-dns.md) 방법에 대 한 지침은 tooconfigure 위임에 대 한 이름 서버입니다. 도메인이 Azure DNS 영역 위임된 tooyour 이면 데 필요한 수 tooconfigure hello DNS 레코드가 됩니다.

[Azure Function Apps](#azure-function-app), [Azure IoT](#azure-iot), [공용 IP 주소](#public-ip-address), [App Service(Web Apps)](#app-service-web-apps), [Blob Storage](#blob-storage) 및 [Azure CDN](#azure-cdn)에 대해 베니티 또는 사용자 지정 도메인을 구성할 수 있습니다.

## <a name="azure-function-app"></a>Azure 함수 앱

Azure 기능 앱에 대 한 사용자 지정 도메인 tooconfigure hello 함수 앱 자체에 구성 뿐만 아니라 CNAME 레코드가 생성 됩니다.
 
너무 이동**다른** > **함수 앱** 함수 응용 프로그램을 선택 합니다. **플랫폼 기능**을 클릭하고 **네트워킹** 아래에서 **사용자 지정 도메인**을 클릭합니다.

![함수 앱 블레이드](./media/dns-custom-domain/functionapp.png)

Hello에 현재 url hello 참고 **사용자 지정 도메인** 블레이드에서이 주소는 만든 hello DNS 레코드에 대 한 hello 별칭으로 사용 됩니다.

![사용자 지정 도메인 블레이드](./media/dns-custom-domain/functionshostname.png)

Tooyour DNS 영역을 이동 하 고 클릭 **집합을 기록해 +**합니다. Hello hello에 다음 정보를 기입 **레코드 집합을 추가** 블레이드에 대 한 클릭 **확인** toocreate 것입니다.

|속성  |값  |설명  |
|---------|---------|---------|
|이름     | myfunctionapp        | 이 값을 도메인 이름 레이블이 hello과 함께 hello 사용자 지정 도메인 이름에 대 한 hello FQDN입니다.        |
|형식     | CNAME        | 별칭을 사용하는 CNAME 레코드를 사용합니다.        |
|TTL     | 1        | 1은 1시간 동안 사용됩니다.        |
|TTL 단위     | 시간        | Hello 시간 측정으로 사용 되는 시간         |
|Alias     | adatumfunction.azurewebsites.net        | hello DNS 이름을 hello 별칭을 만드는에 대 한이 예제 기본 toohello 함수 응용 프로그램에서 제공 하는 hello adatumfunction.azurewebsites.net DNS 이름입니다.        |

뒤로 tooyour 함수 응용 프로그램 이동를 클릭 **플랫폼 기능**, 아래에서 **네트워킹** 클릭 **사용자 지정 도메인**, 다음 **Hostnames**클릭 **+ 호스트 이름 추가**합니다.

Hello에 **호스트 이름 추가** 블레이드에서 hello에 hello CNAME 레코드를 입력 **hostname** 텍스트 필드와 클릭 **유효성 검사**합니다. Hello 레코드를 찾을 수 toobe 되었으면 hello **호스트 이름 추가** 단추가 나타납니다. 클릭 **호스트 이름 추가** tooadd hello 별칭입니다.

![함수 앱 호스트 이름 추가 블레이드](./media/dns-custom-domain/functionaddhostname.png)

## <a name="azure-iot"></a>Azure IoT

Azure IoT는 사용자 지정 내용을 hello 서비스 자체에 필요는 없습니다. IoT Hub를 사용 하 여 사용자 지정 도메인 toouse toohello 리소스를 가리키는 CNAME 레코드에만 필요 합니다.

너무 이동**사물 인터넷** > **IoT Hub** IoT 허브를 선택 합니다. Hello에 **개요** 블레이드에서 참고 hello hello IoT 허브의 FQDN입니다.

![IoT Hub 블레이드](./media/dns-custom-domain/iot.png)

다음 tooyour DNS 영역을 이동 하 고 클릭 **집합을 기록해 +**합니다. Hello hello에 다음 정보를 기입 **레코드 집합을 추가** 블레이드에 대 한 클릭 **확인** toocreate 것입니다.


|속성  |값  |설명  |
|---------|---------|---------|
|이름     | myiothub        | 이 값을 도메인 이름 레이블이 hello과 함께 hello IoT 허브에 대 한 hello FQDN입니다.        |
|형식     | CNAME        | 별칭을 사용하는 CNAME 레코드를 사용합니다.
|TTL     | 1        | 1은 1시간 동안 사용됩니다.        |
|TTL 단위     | 시간        | Hello 시간 측정으로 사용 되는 시간         |
|Alias     | adatumIOT.azure-devices.net        | hello DNS 이름을 hello 별칭을 만드는에 대 한이 예에서 hello IoT 허브에서 제공 하는 hello adatumIOT.azure devices.net 호스트 이름입니다.

Hello 레코드를 만든 후 사용 하 여 hello CNAME 레코드와 이름 확인을 테스트 합니다.`nslookup`

## <a name="public-ip-address"></a>공용 IP 주소

리소스 관리자 Vm에서 부하 분산 장치, 응용 프로그램 게이트웨이 클라우드 서비스와 같은 리소스 주소를 지정 된 공용 IP를 사용 하는 서비스에 대 한 사용자 지정 도메인 tooconfigure 및 클래식 Vm에 CNAME 레코드를 사용 합니다.

너무 이동**네트워킹** > **공용 IP 주소**hello 공용 IP 리소스를 선택 하 고 클릭 **구성**합니다. Notate hello IP 주소를 표시 합니다.

![공용 ip 블레이드](./media/dns-custom-domain/publicip.png)

Tooyour DNS 영역을 이동 하 고 클릭 **집합을 기록해 +**합니다. Hello hello에 다음 정보를 기입 **레코드 집합을 추가** 블레이드에 대 한 클릭 **확인** toocreate 것입니다.


|속성  |값  |설명  |
|---------|---------|---------|
|이름     | mywebserver        | 이 값을 도메인 이름 레이블이 hello과 함께 hello 사용자 지정 도메인 이름에 대 한 hello FQDN입니다.        |
|형식     | A        | Hello 리소스는 IP 주소 처럼 A 레코드를 사용 합니다.        |
|TTL     | 1        | 1은 1시간 동안 사용됩니다.        |
|TTL 단위     | 시간        | Hello 시간 측정으로 사용 되는 시간         |
|IP 주소     | <your ip address>       | hello 공용 IP 주소입니다.|

![A 레코드 만들기](./media/dns-custom-domain/arecord.png)

Hello A 레코드를 만든 후 실행 `nslookup` toovalidate hello 레코드를 확인 합니다.

![공용 ip dns 조회](./media/dns-custom-domain/publicipnslookup.png)

## <a name="app-service-web-apps"></a>App Service(Web Apps)

hello 다음 단계가 수행 하면 앱 서비스 웹 앱에 대 한 사용자 지정 도메인을 구성 하는 과정입니다.

너무 이동**웹 및 모바일** > **앱 서비스** 사용자 지정 도메인 이름을 구성 하는 하 고 클릭 hello 리소스를 선택 하 고 **사용자 지정 도메인**합니다.

Hello에 현재 url hello 참고 **사용자 지정 도메인** 블레이드에서이 주소는 만든 hello DNS 레코드에 대 한 hello 별칭으로 사용 됩니다.

![사용자 지정 도메인 블레이드](./media/dns-custom-domain/url.png)

Tooyour DNS 영역을 이동 하 고 클릭 **집합을 기록해 +**합니다. Hello hello에 다음 정보를 기입 **레코드 집합을 추가** 블레이드에 대 한 클릭 **확인** toocreate 것입니다.


|속성  |값  |설명  |
|---------|---------|---------|
|이름     | mywebserver        | 이 값을 도메인 이름 레이블이 hello과 함께 hello 사용자 지정 도메인 이름에 대 한 hello FQDN입니다.        |
|형식     | CNAME        | 별칭을 사용하는 CNAME 레코드를 사용합니다. A 레코드 hello 리소스는 IP 주소를 사용 하는 경우 사용 됩니다.        |
|TTL     | 1        | 1은 1시간 동안 사용됩니다.        |
|TTL 단위     | 시간        | Hello 시간 측정으로 사용 되는 시간         |
|Alias     | webserver.azurewebsites.net        | hello DNS 이름을 hello 별칭을 만드는에 대 한이 예제 기본 toohello 웹 응용 프로그램에서 제공 하는 hello webserver.azurewebsites.net DNS 이름입니다.        |


![CNAME 레코드 만들기](./media/dns-custom-domain/createcnamerecord.png)

Hello 사용자 지정 도메인 이름에 대해 구성 된 백 toohello 응용 프로그램 서비스를 이동 합니다. **사용자 지정 도메인**을 클릭한 후 **호스트 이름**을 클릭합니다. 만든 tooadd hello CNAME 레코드를 클릭 **+ 호스트 이름 추가**합니다.

![그림 1](./media/dns-custom-domain/figure1.png)

Hello 프로세스가 완료 되 면 실행 **nslookup** toovalidate 이름 확인이 작동 합니다.

![그림 1](./media/dns-custom-domain/finalnslookup.png)

매핑 사용자 지정 도메인 tooApp 서비스에 대해 자세히 toolearn 방문 [는 기존 사용자 지정 DNS 이름 tooAzure 웹 응용 프로그램을 매핑할](../app-service-web/app-service-web-tutorial-custom-domain.md?toc=%dns%2ftoc.json)합니다.

사용자 지정 도메인 toopurchase 필요 하면 방문 [Azure 웹 앱에 대 한 사용자 지정 도메인 이름을 구매](../app-service-web/custom-dns-web-site-buydomains-web-app.md) toolearn 앱 서비스 도메인에 대 한 자세한 합니다.

## <a name="blob-storage"></a>Blob 저장소

hello 다음 단계가 수행 하면 hello asverify 메서드를 사용 하 여 blob 저장소 계정에 대 한 CNAME 레코드를 구성 하는 과정입니다. 이 메서드는 가동 중지 시간이 없음을 보장합니다.

너무 이동**저장소** > **저장소 계정은**저장소 계정을 선택 하 고 클릭 **사용자 지정 도메인**합니다. 2 단계에서 FQDN hello notate,이 값은 사용 toocreate hello 첫 번째 CNAME 레코드

![Blob Storage 사용자 지정 도메인](./media/dns-custom-domain/blobcustomdomain.png)

Tooyour DNS 영역을 이동 하 고 클릭 **집합을 기록해 +**합니다. Hello hello에 다음 정보를 기입 **레코드 집합을 추가** 블레이드에 대 한 클릭 **확인** toocreate 것입니다.


|속성  |값  |설명  |
|---------|---------|---------|
|이름     | asverify.mystorageaccount        | 이 값을 도메인 이름 레이블이 hello과 함께 hello 사용자 지정 도메인 이름에 대 한 hello FQDN입니다.        |
|형식     | CNAME        | 별칭을 사용하는 CNAME 레코드를 사용합니다.        |
|TTL     | 1        | 1은 1시간 동안 사용됩니다.        |
|TTL 단위     | 시간        | Hello 시간 측정으로 사용 되는 시간         |
|Alias     | asverify.adatumfunctiona9ed.blob.core.windows.net        | hello DNS 이름을 hello 별칭을 만드는에 대 한이 예제 기본 toohello 저장소 계정에서 제공 하는 hello asverify.adatumfunctiona9ed.blob.core.windows.net DNS 이름입니다.        |

뒤로 tooyour 저장소 계정을 클릭 하 여 탐색 **저장소** > **저장소 계정은**저장소 계정을 선택 하 고 클릭 **사용자 지정 도메인**합니다. Hello hello asverify 접두사 hello 텍스트 상자를 검사 하지 않고 만든 별칭에 형식 * * 간접 CNAME 유효성 검사를 사용 하 고 클릭 **저장**합니다. 이 단계가 완료 되 면 tooyour DNS 영역을 반환 하 고 hello asverify 접두사 없이 CNAME 레코드를 만듭니다.  따라서 그 시점 hello cdnverify 접두사로 안전 toodelete hello CNAME 레코드 수 있습니다.

![Blob Storage 사용자 지정 도메인](./media/dns-custom-domain/indirectvalidate.png)

`nslookup`을 실행하여 DNS 확인 유효성 검사

방문 매핑 사용자 지정 도메인 tooa blob 저장소 끝점에 대 한 자세한 toolearn [Blob 저장소 끝점에 대 한 사용자 지정 도메인 이름 구성](../storage/blobs/storage-custom-domain-name.md?toc=%dns%2ftoc.json)

## <a name="azure-cdn"></a>Azure CDN

hello 다음 단계가 수행 하면 hello cdnverify 메서드를 사용 하 여 CDN 끝점에 대 한 CNAME 레코드를 구성 하는 과정입니다. 이 메서드는 가동 중지 시간이 없음을 보장합니다.

너무 이동**네트워킹** > **CDN 프로필**CDN 프로필을 선택 하 고 클릭 **끝점** 아래 **일반**합니다.

Hello 끝점을 사용 하는 하 고 클릭 선택 **+ 사용자 지정 도메인**합니다. 참고 hello **끝점 호스트 이름** 해당 hello CNAME 레코드가 가리키는이 값은 hello 레코드입니다.

![CDN 사용자 지정 도메인](./media/dns-custom-domain/endpointcustomdomain.png)

Tooyour DNS 영역을 이동 하 고 클릭 **집합을 기록해 +**합니다. Hello hello에 다음 정보를 기입 **레코드 집합을 추가** 블레이드에 대 한 클릭 **확인** toocreate 것입니다.

|속성  |값  |설명  |
|---------|---------|---------|
|이름     | cdnverify.mycdnendpoint        | 이 값을 도메인 이름 레이블이 hello과 함께 hello 사용자 지정 도메인 이름에 대 한 hello FQDN입니다.        |
|형식     | CNAME        | 별칭을 사용하는 CNAME 레코드를 사용합니다.        |
|TTL     | 1        | 1은 1시간 동안 사용됩니다.        |
|TTL 단위     | 시간        | Hello 시간 측정으로 사용 되는 시간         |
|Alias     | cdnverify.adatumcdnendpoint.azureedge.net        | hello DNS 이름을 hello 별칭을 만드는에 대 한이 예제 기본 toohello 저장소 계정에서 제공 하는 hello cdnverify.adatumcdnendpoint.azureedge.net DNS 이름입니다.        |

클릭 하 여 뒤로 tooyour CDN 끝점을 탐색 **네트워킹** > **CDN 프로필**, CDN 프로필을 선택 합니다. 클릭 **+ 사용자 지정 도메인** hello cdnverify 접두사 없이 CNAME 레코드 별칭을 입력 하 고 클릭 **추가**합니다.

이 단계가 완료 되 면 tooyour DNS 영역을 반환 하 고 hello cdnverify 접두사 없이 CNAME 레코드를 만듭니다.  따라서 그 시점 hello cdnverify 접두사로 안전 toodelete hello CNAME 레코드 수 있습니다. CDN에 대 한 자세한 내용은 어떻게 tooconfigure hello 중간 등록 단계 없이 사용자 지정 도메인 방문 및 [맵 Azure CDN 콘텐츠 tooa 사용자 지정 도메인](../cdn/cdn-map-content-to-custom-domain.md?toc=%dns%2ftoc.json)합니다.

## <a name="next-steps"></a>다음 단계

너무 방법에 대해 알아봅니다[Azure에서 호스팅된 서비스에 대 한 역방향 DNS 구성](dns-reverse-dns-for-azure-services.md)합니다.
