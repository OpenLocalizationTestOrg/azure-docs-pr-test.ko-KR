---
title: "aaaConfiguration 및 관리 문제를 Microsoft Azure 클라우드 서비스 FAQ | Microsoft Docs"
description: "이 문서에서는 구성 및 Microsoft Azure 클라우드 서비스에 대 한 관리 하는 방법에 대 한 질문과 대답 hello를 나열 합니다."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 62ece142ac0ef5d45081cab333375b1a0a8f0ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-and-management-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Azure Cloud Services의 구성 및 관리 문제: FAQ(질문과 대답)

이 문서는 [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services)의 구성 및 관리 문제에 대한 질문과 대답을 포함합니다. Hello를 참조할 수 있습니다 [클라우드 서비스 VM 크기 페이지](cloud-services-sizes-specs.md) 크기 정보에 대 한 합니다.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="how-do-i-add-nosniff-toomy-website"></a>"Nosniff" toomy 웹 사이트를 추가 하려면 어떻게 해야 합니까?
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

## <a name="how-do-i-customize-iis-for-a-web-role"></a>웹 역할에 IIS를 사용자 지정하려면 어떻게 할까요?
Hello에서 hello IIS 시작 스크립트를 사용 하 여 [일반적인 시작 작업](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) 문서.

## <a name="i-cannot-scale-beyond-x-instances"></a>X 인스턴스 이상 확장할 수 없습니다.
Azure 구독에 코어를 사용할 수 있습니다 hello 수에 대 한 제한입니다. 사용 가능한 모든 hello 코어를 사용한 경우 배율이 작동 하지 않습니다. 예를 들어 100개의 코어 제한이 있으면 클라우드 서비스에 대한 100개의 A1 크기 가상 컴퓨터 인스턴스나 50개의 A2 크기 가상 컴퓨터 인스턴스를 생성할 수 있습니다.

## <a name="how-can-i-implement-role-based-access-for-cloud-services"></a>Cloud Services에 역할 기반 액세스를 구현하려면 어떻게 할까요?
클라우드 서비스는 Azure 리소스 관리자 기반 서비스 이므로 hello 역할 기반 액세스 제어 (RBAC) 모델을 지원 하지 않습니다.

[Azure RBAC와 클래식 구독 관리자 비교](../active-directory/role-based-access-control-what-is.md#azure-rbac-vs-classic-subscription-administrators)를 참조하세요.

## <a name="how-do-i-set-hello-idle-timeout-for-azure-load-balancer"></a>Azure 부하 분산 장치에 대 한 hello 유휴 시간 제한을 설정 하는 방법
다음과 같이 서비스 정의 (csdef) 파일에서 hello 제한 시간을 지정할 수 있습니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="mgVS2015Worker" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2015-04.2.6">
  <WorkerRole name="WorkerRole1" vmsize="Small">
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" />
    </ConfigurationSettings>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <Endpoints>
      <InputEndpoint name="Endpoint1" protocol="tcp" port="10100"   idleTimeoutInMinutes="30" />
    </Endpoints>
  </WorkerRole>
```
자세한 정보는 [새로 만들기: Azure Load Balancer에 구성 가능한 유휴 시간 제한](https://azure.microsoft.com/blog/new-configurable-idle-timeout-for-azure-load-balancer/)을 참조하세요.

## <a name="can-microsoft-internal-engineers-rdp-toocloud-service-instances-without-permission"></a>Microsoft 내부 엔지니어의 허가 없이 RDP toocloud 서비스 인스턴스 수 있습니까?
엄격한 프로세스 내부 허용 하지 않고 클라우드 서비스에 tooRDP 엔지니어 Microsoft 다음과 hello 소유자 또는 해당 지정 된 사용자 권한 (전자 메일 또는 기타 서 면된 통신) 작성.

## <a name="why-is-hello-certificate-chain-of-my-cloud-service-ssl-certificate-incomplete"></a>Hello 인증서 체인 내 클라우드 서비스 SSL 인증서의 전체 없는 이유
Hello 전체 인증서 체인 (리프 인증서, 중간 인증서 및 루트 인증서) 방금 hello 리프 인증서 대신 설치 하는 것이 좋습니다. 방금 hello 리프 인증서를 설치할 때 사용 하면 Windows toobuild hello 인증서 체인 hello CTL을 탐색 하 여 됩니다. 발생 한 경우 일시적인 네트워크 또는 DNS 문제가 Azure 또는 Windows Update에서 toovalidate hello 인증서 하는 동안 Windows hello 인증서 간주 될 수 잘못 되었습니다. Hello 전체 인증서 체인을 설치 하 여이 문제를 방지할 수 있습니다. hello에 블로그 [어떻게 tooinstall 체인된 SSL 인증서를](https://blogs.msdn.microsoft.com/azuredevsupport/2010/02/24/how-to-install-a-chained-ssl-certificate/) 표시 방법을 toodo이 합니다.

## <a name="how-do-i-associate-a-static-ip-address-toomy-cloud-service"></a>고정 IP 주소 toomy 클라우드 서비스에 연결 어떻게 합니까?
고정 IP 주소를 tooset, 예약 된 IP toocreate가 필요합니다. 이 예약 된 IP 연결된 tooa 새 클라우드 서비스 또는 tooan 기존 배포 될 수 있습니다. Hello 다음 세부 정보에 대 한 문서를 참조 하십시오.
* [어떻게 toocreate 예약 된 IP 주소](../virtual-network/virtual-networks-reserved-public-ip.md#manage-reserved-vips)
* [기존 클라우드 서비스의 hello IP 주소를 예약 합니다.](../virtual-network/virtual-networks-reserved-public-ip.md#reserve-the-ip-address-of-an-existing-cloud-service)
* [예약 된 IP tooa 새 클라우드 서비스에 연결](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-new-cloud-service)
* [배포 실행 예약 된 IP tooa 연결](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-running-deployment)
* [서비스 구성 파일을 사용 하 여 예약 된 IP tooa 클라우드 서비스에 연결](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-cloud-service-by-using-a-service-configuration-file)

## <a name="what-is-hello-quota-limit-for-my-cloud-service"></a>클라우드 서비스에 대 한 hello 할당량 한도 무엇입니까?
[서비스 특정 제한](../azure-subscription-service-limits.md#subscription-limits)을 참조하세요.

## <a name="why-does-hello-drive-on-my-cloud-service-vm-show-very-little-free-disk-space"></a>VM 클라우드 서비스에 대해 hello 드라이브 사용 가능한 디스크 공간이 거의 표시 하는 이유
이 동작은 정상적인된 동작 하 고 모든 문제 tooyour 응용 프로그램을 발생 하지 않아야 합니다. Hello %uproot 기본적으로 파일을 정상적으로 차지 하는 공간의 double hello 크기를 사용 하는 Azure PaaS Vm에서 % 드라이브에 대 한 저널링 켜 집니다. 그러나 몇 가지 있는 toobe 기본적으로이으로 전환 문제 비 합니다.

hello %approot% 드라이브 크기 +로 계산 됩니다 < 크기.cspkg + 최대 업무 일지 크기 > 여유 공간의 여백 또는 1.5 g B 중 더 큰 값입니다. VM의 hello 크기가이 계산에 관계가 없습니다. (VM 크기 hello만 영향을 미칩니다 hello 임시 c: 드라이브의 hello 크기를입니다.) 

것은 지원 되지 않는 toowrite toohello %approot% 드라이브입니다. Toohello Azure VM을 작성 하는 경우 그렇게 해야 합니다는 임시 LocalStorage 리소스 (또는 다른 옵션을 Blob 저장소에 Azure Files 등과 합니다.). 따라서 hello 양의 여유 공간 hello %approot% 폴더에는 의미가 없습니다. 응용 프로그램은 toohello %approot% 드라이브를 작성 하는 경우에 확실 하지 않은 몇 일 동안 실행 한 다음 "before" 및 "after" 크기 hello를 비교 하 여 서비스 항상 하도록 할 수 있습니다. 

Azure 아무 것도 작성 하지 것입니다 toohello %approot% 드라이브입니다. Hello VHD가 사용자의.cspkg에서을 만들어 hello Azure VM에 탑재 되 면 hello toothis 드라이브를 작성할 수는 응용 프로그램입니다. 

hello 저널 설정을 구성할 수 없는 되므로에서 끌 수 없습니다.

## <a name="what-are-hello-features-and-capabilities-that-azure-basic-ipsids-and-ddos-provides"></a>Hello 기능 및 특성에 기본 ID IP/Azure와 DDOS 제공 하는 것이 무엇입니까?
Azure IP/ID 위협 으로부터 물리적 서버 toodefend 데이터 센터에 저장 합니다. 또한 고객은 웹 응용 프로그램 방화벽, 네트워크 방화벽, 맬웨어 방지 프로그램, 침입 감지 및 방지 시스템(IDS/IPS) 등과 같은 타사 보안 솔루션을 배포할 수 있습니다. 자세한 내용은 [데이터 및 자산 보호 및 글로벌 보안 표준 준수](https://www.microsoft.com/en-us/trustcenter/Security/AzureSecurity)를 참조하세요.

Microsoft에서는 서버, 네트워크 및 응용 프로그램 toodetect 위협 지속적으로 모니터링 합니다. Azure의 multipronged 위협 관리 방법은 침입 감지를 사용 하 여, 분산된의 서비스 거부 (DDoS) 공격 방지, 침투, 동작 분석, 이상 탐지 및 기계 학습 tooconstantly의 철저 한 방어를 강화 고 위험을 줄입니다. Azure용 Microsoft 맬웨어 방지 프로그램은 Azure Cloud Services 및 가상 컴퓨터를 보호합니다. 웹 응용 프로그램 화재 벽, 네트워크 방화벽, 맬웨어 방지, 침입 검색 및 방지 시스템 ID/IP (), 등과 같은 hello 옵션 toodeploy 제 3 자 보안 해결책을 또한 사용할 합니다.

## <a name="why-does-iis-stop-writing-toohello-log-directory"></a>이유는 IIS 중지 toohello 로그 디렉터리 쓰기?
Toohello 로그 디렉터리를 작성 하기 위한 로컬 저장소 할당량 hello를 모두 사용 했습니다. 이를 수정하기 위해 다음 세 가지 중 하나를 수행할 수 있습니다.
* IIS에 대 한 진단을 사용 하도록 설정 하 고 hello 주기적으로 이동 하는 진단 tooblob 저장소를 갖습니다.
* 디렉터리 로깅 hello에서 로그 파일을 수동으로 제거 합니다.
* 로컬 리소스에 대한 할당량 제한을 늘립니다.

자세한 내용은 다음 문서는 hello를 참조 하세요.
* [Azure Storage에서 진단 데이터 저장 및 보기](cloud-services-dotnet-diagnostics-storage.md)
* [클라우드 서비스에서 IIS 로그 작성 중지](https://blogs.msdn.microsoft.com/cie/2013/12/21/iis-logs-stops-writing-in-cloud-service/)

## <a name="what-is-hello-purpose-of-hello-windows-azure-tools-encryption-certificate-for-extensions"></a>"Windows Azure Tools 암호화 인증서에 대 한 확장" hello의 hello 목적은 이란?
이러한 인증서 확장 toohello 클라우드 서비스에 추가 될 때마다 자동으로 만들어집니다. 가장 일반적으로이 hello WAD 확장 또는 hello RDP 확장 이지만 hello 로그 수집기 또는 맬웨어 방지 확장 등 다른 사용자에 게 수도 있습니다. 이러한 인증서는 암호화 및 해독 하는 hello 확장에 대 한 hello 개인 구성에만 사용 됩니다. hello 만료 날짜는 하지 않습니다 확인 hello 인증서 만료 되 면 문제가 되지 않습니다. 

이러한 인증서를 무시할 수 있습니다. Hello 인증서를 정리 하려면 모든 삭제를 시도할 수 있습니다. Azure는 오류를 throw toodelete 하면 사용 중인 인증서입니다.

## <a name="how-can-i-generate-a-certificate-signing-request-csr-without-rdp-ing-in-toohello-instance"></a>Toohello 인스턴스에서 CSR 인증서 서명 요청 () "RDP ing" 하지 않고는 어떻게 생성할 수 있습니까?
다음 지침 문서 hello 참조:

>[WAWS(Windows Azure 웹 사이트)를 사용하기 위해 인증서 가져오기](https://azure.microsoft.com/blog/obtaining-a-certificate-for-use-with-windows-azure-web-sites-waws/)

CSR은 텍스트 파일입니다. 없는 hello 컴퓨터에서 만든 toobe hello 인증서가 궁극적으로 사용 됩니다. 이 문서는 응용 프로그램 서비스에 대 한 작성, 있지만 hello CSR 만들기는 제네릭 및 클라우드 서비스에도 적용 됩니다.
