---
title: "Azure 저장소와 함께 사용할 수 있는 aaaSecurity 기능 | Microsoft Docs"
description: " 이 문서에서는 Azure 저장소에 사용할 수 있는 hello 핵심 Azure 보안 기능의 개요를 제공 합니다. "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 521180dc-2cc9-43f1-ae87-2701de7ca6b8
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 663cd2705527957d21ff9475a6322b42a16c95e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-security-overview"></a>Azure 저장소 보안 개요
Azure 저장소는 내구성, 가용성 및 고객의 확장성 toomeet hello 요구를 사용 하는 최신 응용 프로그램에 대 한 hello 클라우드 저장소 솔루션입니다. Azure 저장소는 포괄적인 보안 기능 집합을 제공합니다.

* 역할 기반 액세스 제어 및 Azure Active Directory를 사용 하 여 hello 저장소 계정을 보호할 수 있습니다.
* 클라이언트 쪽 암호화, HTTP 또는 SMB 3.0을 사용하여 응용 프로그램과 Azure 간에 전송 중인 데이터의 보안을 유지할 수 있습니다.
* 데이터 toobe 자동으로 암호화를 설정할 수 있습니다 때 tooAzure 저장소 서비스 암호화를 사용 하 여 저장소를 기록 합니다.
* 가상 컴퓨터에서 사용 되는 OS 및 데이터 디스크 toobe Azure 디스크 암호화를 사용 하 여 암호화를 설정할 수 있습니다.
* 공유 액세스 서명을 사용 하 여 Azure 저장소에 toohello 데이터 개체를 위임 된 액세스를 부여할 수 있습니다.
* Storage analytics를 사용 하 여 저장소에 액세스할 때 사용자가 사용 하는 hello 인증 방법을 추적할 수 있습니다.

Azure 저장소에 보안에 대해 보다 자세한, 참조 hello [Azure 저장소 보안 가이드](../storage/common/storage-security-guide.md)합니다. 이 가이드에서는 데이터 암호화 및 저장소 분석 및 나머지 부분에서는 전송 중에 저장소 계정 키와 같은 Azure 저장소의 hello 보안 기능에 심층 분석을 제공 합니다.

이 문서에서는 Azure Storage에서 사용할 수 있는 Azure 보안 기능의 개요를 제공합니다. 링크에 자세히 알아볼 수 있도록 각 기능에 대 한 세부 정보를 제공 하는 tooarticles를 제공 됩니다.

이 문서에서 다루는 hello 코어 기능 toobe 다음과 같습니다.

* 역할 기반 액세스 제어
* 위임 된 액세스 toostorage 개체
* 전송 중 암호화
* 휴지 상태의 암호화/저장소 서비스 암호화
* Azure 디스크 암호화
* Azure Key Vault

## <a name="role-based-access-control-rbac"></a>역할 기반 액세스 제어(RBAC)
RBAC(역할 기반 액세스 제어)를 사용하여 저장소 계정의 보안을 유지할 수 있습니다. Hello에 따라 액세스를 제한 [tooknow 필요](https://en.wikipedia.org/wiki/Need_to_know) 및 [최소 권한](https://en.wikipedia.org/wiki/Principle_of_least_privilege) 보안 주체는 데이터 액세스를 위한 보안 정책 tooenforce는 조직을 위한 것입니다. 적절 한 RBAC 역할 toogroups hello 및 특정 범위의 응용 프로그램을 할당 하 여 이러한 액세스 권한이 부여 됩니다. 사용할 수 있습니다 [기본 제공 RBAC 역할](../active-directory/role-based-access-built-in-roles.md), 저장소 계정 참가자와 같은 tooassign 권한 toousers 합니다.

자세한 정보:

* [Azure Active Directory 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)

## <a name="delegated-access-toostorage-objects"></a>위임 된 액세스 toostorage 개체
공유 액세스 서명 (SAS) 저장소 계정에 tooresources 위임 된 액세스를 제공합니다. hello SAS 클라이언트 시간 및 지정한 사용 권한 집합으로 지정된 된 기간에 대 한 저장소 계정에 사용 권한을 tooobjects 제한에 부여할 수 있는 것을 의미 합니다. 계정 액세스 키 tooshare 필요 없이 이러한 제한 된 사용 권한을 부여할 수 있습니다. hello SAS 쿼리 매개 변수에서 인증 된 액세스 tooa 저장소 리소스에 대해 필요한 모든 hello 정보를 포함 하는 URI입니다. SAS hello로 저장소 리소스 tooaccess hello 클라이언트 tooprovide hello SAS toohello 적절 한 생성자 또는 메서드에만 필요합니다.

자세한 정보:

* [Hello SAS 모델 이해](../storage/common/storage-dotnet-shared-access-signature-part-1.md)
* [Blob 저장소와 함께 SAS 만들기 및 사용](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md)

## <a name="encryption-in-transit"></a>전송 중 암호화
전송 중 암호화는 네트워크를 통해 전송되는 경우 데이터 보호의 메커니즘입니다. Azure 저장소와 함께 다음을 사용하여 데이터를 보호할 수 있습니다.

* [전송 수준 암호화](../storage/common/storage-security-guide.md#encryption-in-transit)(예: Azure 저장소 안팎으로 데이터를 전송하는 경우 HTTPS)
* [실시간 암호화](../storage/common/storage-security-guide.md#using-encryption-during-transit-with-azure-file-shares)(예: Azure 파일 공유에 대한 SMB 3.0 암호화)
* [클라이언트 쪽 암호화](../storage/common/storage-security-guide.md#using-client-side-encryption-to-secure-data-that-you-send-to-storage), tooencrypt hello 데이터 저장소에서 전송 된 후 저장소 및 toodecrypt hello 데이터로 전송 될 때까지 합니다.

클라이언트 쪽 암호화에 대해 자세히 알아봅니다.

* [Microsoft Azure 저장소용 클라이언트 쪽 암호화](https://blogs.msdn.microsoft.com/windowsazurestorage/2015/04/28/client-side-encryption-for-microsoft-azure-storage-preview/)
* [클라우드 보안 컨트롤 시리즈: 전송 중인 데이터 암호화](http://blogs.microsoft.com/cybertrust/2015/08/10/cloud-security-controls-series-encrypting-data-in-transit/)

## <a name="encryption-at-rest"></a>휴지 상태의 암호화
여러 조직에서 [미사용 데이터 암호화](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) 는 데이터 프라이버시, 규정 준수 및 데이터 주권을 위한 필수 단계입니다. “휴지 상태”의 데이터 암호화를 제공하는 세 가지 Azure 기능이 있습니다.

* [저장소 서비스 암호화](../storage/common/storage-security-guide.md#encryption-at-rest) toorequest hello 저장소 서비스 tooAzure 저장소를 작성할 때 자동으로 데이터를 암호화를 사용 하면 됩니다.
* [클라이언트 쪽 암호화](../storage/common/storage-security-guide.md#client-side-encryption) 미사용 데이터 암호화의 hello 기능을 사용 합니다.
* [Azure 디스크 암호화](../storage/common/storage-security-guide.md#using-azure-disk-encryption-to-encrypt-disks-used-by-your-virtual-machines) tooencrypt hello OS 디스크 및 데이터 디스크는 IaaS 가상 컴퓨터에서 사용 하는 사용자에 게 있습니다.

저장소 서비스를 암호화에 대해 자세히 알아봅니다.

* [Azure Blob 저장소](https://azure.microsoft.com/services/storage/blobs/)에 [Azure 저장소 서비스 암호화](https://azure.microsoft.com/services/storage/)를 사용할 수 있습니다. 다른 Azure Storage 형식에 대한 자세한 내용은 [파일](https://azure.microsoft.com/services/storage/files/), [디스크(Premium Storage)](https://azure.microsoft.com/services/storage/premium-storage/), [테이블](https://azure.microsoft.com/services/storage/tables/) 및 [큐](https://azure.microsoft.com/services/storage/queues/)를 참조하세요.
* [휴지 상태의 데이터에 대한 Azure 저장소 서비스 암호화](../storage/common/storage-service-encryption.md)

## <a name="azure-disk-encryption"></a>Azure 디스크 암호화
VM(가상 컴퓨터)에 대한 Azure 디스크 암호화는 [Azure 주요 자격 증명 모음](https://azure.microsoft.com/services/key-vault/)에서 제어하는 키와 정책으로 VM 디스크(부팅 및 데이터 디스크 포함)를 암호화하여 조직 보안 및 규정 준수 요구 사항을 처리할 수 있도록 도와줍니다.

VM에 대한 디스크 암호화는 Linux 및 Windows 운영 체제에 적합합니다. 또한 주요 자격 증명 모음 toohelp 보호, 관리 및 디스크 암호화 키의 사용을 감사 하기를 사용 합니다. VM 디스크에 모든 hello 데이터는 Azure 저장소 계정에서 업계 표준 암호화 기술을 사용 하 여 휴지 암호화 됩니다. Windows 용 디스크 암호화 솔루션 hello 기반 [Microsoft BitLocker 드라이브 암호화](https://technet.microsoft.com/library/cc732774.aspx), hello Linux 솔루션 기반을 [dm crypt](https://en.wikipedia.org/wiki/Dm-crypt)합니다.

자세한 정보:

* [Windows 및 Linux IaaS Virtual Machines에 대한 Azure 디스크 암호화(영문)](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0)

## <a name="azure-key-vault"></a>Azure 키 자격 증명 모음
Azure 디스크 암호화를 사용 하 여 [Azure 키 자격 증명 모음](https://azure.microsoft.com/services/key-vault/) toohelp 제어 및 관리 디스크 암호화 키 및 비밀 키 자격 증명 모음 구독에서 Azure의 hello 가상 컴퓨터 디스크에서 모든 데이터가 암호화 되는 동시에 저장소입니다. 키 자격 증명 모음 tooaudit 키 및 정책 사용 현황을 사용 해야 합니다.

자세한 정보:

* [Azure 주요 자격 증명 모음이란?](../key-vault/key-vault-whatis.md)
* [Azure 주요 자격 증명 모음 시작](../key-vault/key-vault-get-started.md)
