---
title: "클라우드 서비스 역할 aaaAzure FAQ | Microsoft Docs"
description: "Azure Cloud Services에 대한 질문과 대답입니다. 인증서, 웹 역할 및 작업자 역할에 대한 몇 가지 일반적인 질문의 답변이 제공됩니다."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: b07a1990e031e60ae919a5f7c636945b89c7d3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-services-faq"></a>클라우드 서비스 FAQ
이 문서는 Microsoft Azure 클라우드 서비스에 대한 일부 자주 묻는 질문을 답변합니다. Hello를 방문할 수도 [Azure 지원 FAQ](http://go.microsoft.com/fwlink/?LinkID=185083) 일반적인 Azure 가격 책정 및 지원 정보입니다. Hello를 참조할 수 있습니다 [클라우드 서비스 VM 크기 페이지](cloud-services-sizes-specs.md) 크기 정보에 대 한 합니다.

## <a name="certificates"></a>인증서
### <a name="where-should-i-install-my-certificate"></a>어디에 내 인증서를 설치해야 하나요?
* **내**  
  개인 키를 포함한 응용 프로그램 인증서(\*.pfx, \*.p12)
* **CA**  
  모든 중간 인증서를 이 저장소(정책 및 하위 CA)로 이동시킵니다.
* **루트**  
  기본 루트 CA 인증서 여기로 이동 해야 하므로 hello 루트 CA 저장소입니다.

### <a name="i-cant-remove-expired-certificate"></a>만료된 인증서를 제거할 수 없습니다.
Azure에서는 사용 중인 인증서를 제거할 수 없습니다. Hello 인증서를 사용 하는 tooeither delete hello 배포 또는 다른 또는 갱신 된 인증서로 업데이트 hello 배포 해야 합니다.

### <a name="delete-an-expired-certificate"></a>만료된 인증서 삭제
Hello hello 인증서가 사용 하 여에으로 사용할 수 있습니다 [제거 AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet tooremove 인증서입니다.

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a>확장명이 Windows Azure 서비스 관리라는 인증서가 만료되었습니다.
이러한 인증서는 확장 hello 원격 데스크톱 확장 같은 toohello 클라우드 서비스에 추가 될 때마다 생성 됩니다. 이러한 인증서는 암호화 및 해독 hello hello 확장 개인 구성에만 사용 됩니다. 이러한 인증서가 만료되는 경우 중요하지 않습니다. hello 만료 날짜를 확인 하지 않습니다.

### <a name="certificates-i-have-deleted-keep-reappearing"></a>삭제한 인증서가 다시 나타납니다.
대개 Visual Studio와 같은 사용 중인 도구 때문에 계속 다시 나타납니다. 인증서를 사용 하는 도구와 다시 연결 될 때마다 다시 업로드 tooAzure 수 있습니다.

### <a name="my-certificates-keep-disappearing"></a>내 인증서가 자꾸 없어집니다.
Hello 가상 컴퓨터 인스턴스를 재활용할 때 모든 로컬 변경 내용이 손실 됩니다. 사용 하 여 한 [시작 작업](cloud-services-startup-tasks.md) tooinstall 인증서 toohello 가상 컴퓨터가 각 시간 hello 역할 시작 합니다.

### <a name="i-cannot-find-my-management-certificates-in-hello-portal"></a>Hello 포털에서 관리 인증서를 찾을 수 없습니다
[관리 인증서](../azure-api-management-certs.md) 은 hello Azure 클래식 포털에서에서 사용할 수 있습니다. hello 현재 Azure 포털에서 관리 인증서를 사용 하지 않습니다. 

### <a name="how-can-i-disable-a-management-certificate"></a>어떻게 하면 관리 인증서를 사용하지 않도록 설정할 수 있습니까?
[관리 인증서](../azure-api-management-certs.md) 는 사용하지 않도록 설정할 수 없습니다. 삭제할 hello Azure 클래식 포털을 통해 수 없도록 할 때 toobe 더 이상 사용 합니다.

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a>특정 IP 주소에 대한 SSL 인증서를 만들려면 어떻게 해야 합니까?
Hello의 지시를 hello [인증서 자습서 만들](cloud-services-certs-create.md)합니다. DNS 이름 hello hello IP 주소를 사용 합니다.

## <a name="security"></a>보안
### <a name="disable-ssl-30"></a>SSL 3.0 사용 안 함
toodisable SSL 3.0 및 TLS 보안 사용이 블로그 게시물에 설명 되어 있는 시작 작업을 만듭니다: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/

### <a name="add-nosniff-tooyour-website"></a>추가 **nosniff** tooyour 웹 사이트
hello MIME 형식이 감지 로부터 tooprevent 클라이언트에 설정을 추가 하면 *web.config* 파일입니다.

```xml
<configuration>
   <system.webServer>
      <httpProtocol>
         <customHeaders>
            <add name="X-Content-Type-Options" value="nosniff" />
         </customHeaders>
      </httpProtocol>
   </system.webServer>
</configuration>
```

IIS에서 설정으로도 추가할 수 있습니다. Hello로 사용 하 여 hello 다음 명령은 [일반적인 시작 작업](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) 문서.

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

### <a name="customize-iis-for-a-web-role"></a>웹 역할에 대해 IIS 사용자 지정
Hello에서 hello IIS 시작 스크립트를 사용 하 여 [일반적인 시작 작업](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) 문서.

## <a name="scaling"></a>확장
### <a name="i-cannot-scale-beyond-x-instances"></a>X 인스턴스 이상 확장할 수 없습니다.
Azure 구독에 코어를 사용할 수 있습니다 hello 수에 대 한 제한입니다. 사용 가능한 모든 hello 코어를 사용한 경우 배율이 작동 하지 않습니다. 예를 들어 100개의 코어 제한이 있으면 클라우드 서비스에 대한 100개의 A1 크기 가상 컴퓨터 인스턴스나 50개의 A2 크기 가상 컴퓨터 인스턴스를 생성할 수 있습니다.

## <a name="networking"></a>네트워킹
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a>여러 VIP 클라우드 서비스에서 IP를 예약할 수 없습니다.
먼저, tooreserve hello IP를 만들려고 하는 hello 가상 컴퓨터 인스턴스의 켜져 있는지 확인 합니다. 둘째, 여기 hello 스테이징 및 프로덕션 배포에 대 한 예약 된 Ip를 사용 하는 확인 합니다. **없는** hello 배포를 업그레이드 하는 동안 hello 설정을 변경 합니다.

## <a name="remote-desktop"></a>원격 데스크톱
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a>NSG가 있을 때 원격 데스크톱을 어떻게 수행하나요?
포트에서 트래픽을 허용 하는 NSG 규칙 toohello 추가 **3389** 및 **20000**합니다.  원격 데스크톱은 포트 **3389**를 사용합니다.  클라우드 서비스 인스턴스 부하 분산이 되므로 어떤 인스턴스 tooconnect을 직접 제어할 수 없습니다.  hello *RemoteForwarder* 및 *RemoteAccess* 에이전트 RDP 트래픽을 관리 하 고 hello 클라이언트 toosend RDP 쿠키를 허용 및는 개별 인스턴스 tooconnect를 지정 합니다.  hello *RemoteForwarder* 및 *RemoteAccess* 에이전트에 해당 포트 필요 **20000*** 열 수 있는 NSG 있는 경우 차단 될 수 있습니다.
