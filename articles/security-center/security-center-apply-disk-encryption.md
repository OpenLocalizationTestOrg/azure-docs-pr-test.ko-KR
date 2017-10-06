---
title: "Azure 보안 센터에서 aaaApply 디스크 암호화 | Microsoft Docs"
description: "이 문서에서는 어떻게 tooimplement hello Azure 보안 센터 권장 * * 디스크 암호화 * * 적용 합니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 6cc7824a-8d6b-4a5f-ab40-e3bbaebc4a91
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: cd803f1120018c5c86da91186eec1e59d425ede7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-disk-encryption-in-azure-security-center"></a>Azure 보안 센터에서 디스크 암호화 적용
Azure Security Center는 암호화되지 않은 Windows 또는 Linux VM 디스크가 있는 경우 Azure Disk Encryption을 사용하여 디스크 암호화를 적용하도록 권장합니다. 디스크 암호화를 사용하면 Windows 및 Linux IaaS VM 디스크를 암호화할 수 있습니다.  Hello OS와 VM에 데이터 볼륨에 대 한 암호화를 사용 하는 것이 좋습니다.

디스크 암호화 hello 업계 표준을 사용 하 여 [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) 창과 hello의 기능 [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) Linux의 기능입니다. 이러한 기능은 제공 OS 및 데이터 암호화 toohelp 보호 및 데이터를 보호 하 고 조직의 보안 및 규정 준수 약정을 충족 합니다. 디스크 암호화와 통합 되어 [Azure 키 자격 증명 모음](https://azure.microsoft.com/documentation/services/key-vault/) toohelp 제어 및 관리 hello 디스크 암호화 키 및 비밀 키 자격 증명 모음 구독에서 프로그램 의helloVM디스크에모든데이터를암호화는확인한후에[ Azure 저장소](https://azure.microsoft.com/documentation/services/storage/)합니다.

> [!NOTE]
> Azure 디스크 암호화는 hello 다음 Windows server 운영 체제-Windows Server 2008 R2, Windows Server 2012 및 Windows Server 2012 r 2에서 지원 됩니다. 디스크 암호화는 hello 다음 Linux 서버 운영 체제-Ubuntu, CentOS, SUSE, 및 SUSE Linux Enterprise Server (SLES)에서 지원 됩니다.
>
>

## <a name="implement-hello-recommendation"></a>Hello 권장 구성 구현
1. Hello에 **권장 사항을** 블레이드를 **디스크 암호화 적용**합니다.
2. Hello에 **디스크 암호화 적용** 블레이드에 Vm 디스크 암호화는이 목록을 표시 합니다.
3. Hello 지침 tooapply 암호화 toothese Vm을 따릅니다.

![][1]

보안 센터에서 암호화는 것으로 확인 된 Azure 가상 컴퓨터 tooencrypt 단계를 수행 하는 hello를 권장 됩니다.

* Azure PowerShell을 설치하고 구성합니다. 그러면 toorun hello PowerShell 명령을 필요한 tooset hello 필수 구성 요소 필요 tooencrypt Azure 가상 컴퓨터를 수 있습니다.
* 받으며 hello Azure 디스크 암호화 필수 구성 요소가 Azure PowerShell 스크립트를 실행 합니다.
* 가상 컴퓨터 암호화

[Azure Virtual Machine 암호화](security-center-disk-encryption.md)에서 이러한 단계를 안내합니다.  이 항목에서는 Windows 10을 사용 하는 디스크 암호화를 구성 하는 hello 클라이언트 컴퓨터로 가정 합니다.

Azure Virtual Machines에 대해 사용할 수 있는 방법은 여러 가지가 있습니다. 이미 Azure PowerShell 또는 Azure CLI 잘 알고 있다면 toouse 대체 방법을 할 수도 있습니다. 이러한 다른 방법에 대 한 toolearn 참조 [Azure 디스크 암호화](../security/azure-security-disk-encryption.md)합니다.

## <a name="see-also"></a>참고 항목
이 문서에 설명 했습니다 어떻게 tooimplement hello 보안 센터 권장 사항 "적용 디스크 암호화 합니다." 디스크 암호화에 대해 자세히 toolearn hello 다음을 참조 합니다.

* [Azure 키 자격 증명 암호화 및 키 관리](https://azure.microsoft.com/documentation/videos/azurecon-2015-encryption-and-key-management-with-azure-key-vault/) (비디오, 36 분 39 초)-IaaS Vm 및 Azure 키 자격 증명 모음 toohelp 보호 하 고 데이터를 보호에 대 한 암호화 관리 toouse 디스크 하는 방법에 대해 알아봅니다.
* [Azure 가상 컴퓨터를 암호화](security-center-disk-encryption.md) (문서)-자세한 방법을 tooencrypt Azure 가상 컴퓨터.
* [Azure 디스크 암호화](../security/azure-security-disk-encryption.md) (문서)-tooenable Windows 및 Linux Vm에 대 한 암호화 디스크 하는 방법에 대해 알아봅니다.

보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.

* [Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -자세한 방법을 tooconfigure 보안 정책입니다.
* [Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.
* [Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) -- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.
* [Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -- Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.

<!--Image references-->
[1]: ./media/security-center-apply-disk-encryption/apply-disk-encryption.png
