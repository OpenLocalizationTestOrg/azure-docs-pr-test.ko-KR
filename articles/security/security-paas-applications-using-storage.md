---
title: "Azure 저장소를 사용 하 여 aaaSecuring PaaS 응용 프로그램 | Microsoft Docs"
description: " PaaS 웹 및 모바일 응용 프로그램 보안을 위한 Azure Storage 보안 모범 사례에 대해 알아봅니다. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: TomShinder
ms.openlocfilehash: 3fed75cb121e7f32eb8b948ee12ca35fb25eca7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-web-and-mobile-applications-using-azure-storage"></a>Azure Storage를 사용하여 PaaS 웹 및 모바일 응용 프로그램 보안
이 문서에서는 PaaS 웹 및 모바일 응용 프로그램 보안을 위한 Azure Storage 보안 모범 사례에 대해 설명합니다. 이들 모범 사례는 Azure에 대 한 경험 및 고객의 hello 경험을와 같은 직접 합니다.

hello [Azure 저장소 보안 가이드](../storage/common/storage-security-guide.md) 은 Azure 저장소 및 보안에 대 한 자세한 정보에 대 한 훌륭한 소스입니다.  이 문서에서는 높은 수준의 hello 보안 가이드 및 링크 toohello 보안 가이드 뿐만 아니라 자세한 정보에 대 한 다른 원본에서 발견 된 hello 개념 중 일부입니다.

## <a name="azure-storage"></a>Azure 저장소
Azure를 통해 toodeploy 및 사용 가능한 저장소 방식에서 온 프레미스 쉽게 달성할 수 있습니다. Azure Storage를 사용하면 비교적 적은 노력으로 높은 수준의 확장성 및 가용성을 얻을 수 있습니다. Azure 저장소 hello foundation은 뿐만 아니라 Windows 및 Linux Azure 가상 컴퓨터도 지원할 수 대규모 분산된 응용 프로그램입니다.

Azure 저장소는 다음 4 개의 서비스는 hello 제공: Blob 저장소, 테이블 저장소, 큐 저장소 및 파일 저장소. toolearn 더 참조 [Azure 저장소 소개 tooMicrosoft](../storage/storage-introduction.md)합니다.

## <a name="best-practices"></a>모범 사례
이 문서의 최선의 구현 방법을 hello를 해결할 수 있습니다.

- 액세스 보호:
   - 공유 액세스 서명(SAS)
   - Managed Disk
   - 역할 기반 액세스 제어(RBAC)

- 저장소 암호화:
   - 고가치 데이터에 대한 클라이언트 쪽 암호화
   - 가상 컴퓨터에 대한 Azure Disk Encryption
   - 저장소 서비스 암호화

## <a name="access-protection"></a>액세스 보호
### <a name="use-shared-access-signature-instead-of-a-storage-account-key"></a>저장소 계정 키 대신 공유 액세스 서명 사용

일반적으로 Windows Server 또는 Linux 가상 컴퓨터를 실행하는 IaaS 솔루션에서 파일은 액세스 제어 메커니즘을 사용하여 노출 및 변조 위협으로부터 보호됩니다. Windows에서는 [ACL(액세스 제어 목록)](../virtual-network/virtual-networks-acl.md), Linux에서는 [chmod](https://en.wikipedia.org/wiki/Chmod)를 사용할 수 있습니다. 기본적으로 이 작업은 사용자 고유의 데이터 센터에 있는 서버에서 파일을 보호하는 경우에 수행하는 작업입니다.

PaaS는 다릅니다. Microsoft Azure의 hello 가장 일반적인 방법으로 toostore 파일 중 하나는 toouse [Azure Blob 저장소](../storage/storage-dotnet-how-to-use-blobs.md)합니다. Blob 저장소 및 기타 파일 저장소 간의 차이 hello 파일 I/O 및 파일 I/O와 함께 제공 되는 hello 보호 방법이 됩니다.

액세스 제어는 중요합니다. toohelp tooAzure 저장소 액세스를 제어, hello 시스템에서 생성 두 개의 512 비트 저장소 계정 키 (SAKs) 경우 있습니다 [저장소 계정 만들기](../storage/common/storage-create-storage-account.md)합니다. hello 중복 수준에 키 사용 하면 tooavoid 서비스 인터럽트에 대 한 일상적인 키 회전 하는 동안 있습니다.

저장소 액세스 키는 우선 순위가 높은 비밀 및 액세스할 수 있는 toothose 저장소 액세스 제어에 대 한 책임만 있어야 합니다. 경우 hello 다른 사람이 액세스 toothese 키은 됩니다 완전 하 게 제어할 저장소 및 바꾸기, 삭제 하거나 추가할 수 파일 toostorage 합니다. 여기에는 조직 또는 고객에게 손상을 줄 수 있는 맬웨어 및 다른 유형의 콘텐츠가 포함됩니다.

저장소의 방식으로 tooprovide 액세스 tooobjects를 보내야합니다. tooprovide 보다 세부적인 액세스 하면 활용할 수 [공유 액세스 서명을](../storage/common/storage-dotnet-shared-access-signature-part-1.md) (SAS). hello SAS 쉽게 처리할 수 있습니다 tooshare 저장소에서 특정 개체에 대 한 미리 정의 된 시간 간격에 대 한 고 특정 권한을 부여 합니다. 공유 액세스 서명을 toodefine가 있습니다.

- SAS는 hello를 통해 유효한 hello 시작 시간 및 hello 만료 시간을 포함 하는 hello 간격입니다.
- hello hello SAS 부여 된 사용 권한입니다. 예를 들어 blob SAS 수 사용자 읽기 권한을 부여 및 권한 toothat blob 쓰지만 삭제 권한은 부여 하지 합니다.
- 선택적 IP 주소 또는 IP 주소 범위를 Azure 저장소 허용 SAS hello 합니다. 예를 들어 tooyour 조직에 속한 IP 주소를 지정할 수 있습니다. 이것은 SAS에 대한 보안의 또 다른 측정값을 제공합니다.
- Azure 저장소는 hello SAS를 허용 하는 hello 프로토콜입니다. HTTPS를 사용 하 여이 선택적 매개 변수 toorestrict 액세스 tooclients를 사용할 수 있습니다.

SAS 있습니다 tooshare 원하는 tooshare 콘텐츠 hello 방식으로 저장소 계정 키를 제공 하지 않고 있습니다. 항상 SAS를 사용 하 여 응용 프로그램에 안전 하 게 tooshare 저장소 계정 키를 손상 시 키 지 않고 저장소 리소스는 합니다.

toolearn 더 참조 [공유 액세스 서명을 사용 하 여](../storage/common/storage-dotnet-shared-access-signature-part-1.md) (SAS). 이러한 위험을 toolearn 잠재적 위험 및 권장 사항 toomitigate에 대 한 자세한 참조 [SAS를 사용 하는 경우 최선의 구현 방법](../storage/common/storage-dotnet-shared-access-signature-part-1.md)합니다.

### <a name="use-managed-disks-for-vms"></a>VM에 Managed Disks 사용

선택 하는 경우 [Azure 관리 되는 디스크](../storage/storage-managed-disks-overview.md), Azure가 VM 디스크를 사용 하는 hello 저장소 계정을 관리 합니다. Toodo 있으면 디스크 (프리미엄 또는 표준)와 hello 디스크 크기; hello 유형 선택 Azure 저장소 작업을 수행 합니다 rest hello 합니다. Tooworry 해야 했을 것 그렇지 않으면 tooyou toomultiple 저장소 계정 확장성 제한에 대 한 필요는 없습니다.

toolearn 더 참조 [관리 고 프리미엄 디스크 관리 되지 않는 리소스에 대 한 질문과 대답](../storage/storage-faq-for-disks.md)합니다.

### <a name="use-role-based-access-control"></a>역할 기반 액세스 제어 사용

이전 계정 저장소 계정 키를 노출 하지 않고 저장소 계정 tooother 클라이언트에서 공유 액세스 서명 (SAS) toogrant 제한 된 액세스 tooobjects를 사용 하 여 설명 합니다. 경우에 따라 저장소 계정에 대해 특정 작업과 관련 된 hello 위험 sa hello 이점을 보다 더 큽니다. 경우에 따라 다른 방법으로 toomanage 액세스를 더 간단 합니다.

또 다른 방법은 toomanage 액세스는 toouse [신속히 알아봅니다 액세스 제어](../active-directory/role-based-access-control-what-is.md) (RBAC). RBAC, 직원에 게 필요한 hello 정확 하 게 사용 권한이 부여에 집중 된 hello 필요 tooknow 및 최소 권한의 보안 원칙에 따라. 너무 많은 권한을 계정 tooattackers를 노출할 수 있습니다. 권한이 너무 적으면 직원이 업무를 효율적으로 수행할 수 없습니다. RBAC는 Azure에 대한 세밀한 액세스 관리를 제공하여 이 문제를 해결하도록 도와줍니다. 데이터 액세스를 위한 보안 정책 tooenforce 하려는 조직에 필수적입니다.

Azure tooassign 권한 toousers 있는 기본 제공 RBAC 역할을 활용할 수 있습니다. 클라우드 운영자는 toomanage 저장소 계정 및 클래식 저장소 계정을 참가자 역할 toomanage 클래식 저장소 계정이 필요로 하는 대 한 저장소 계정 참가자를 사용 하는 것이 좋습니다. 필요한 Vm toomanage 있지만 hello 가상 네트워크가 아니라 연결 된 저장소 계정 toowhich 클라우드 연산자에 대 한 toohello 가상 컴퓨터 참가자 역할을 추가 하는 것이 좋습니다.

RBAC 같은 기능을 활용하여 데이터 액세스 제어를 적용하지 않는 조직은 사용자에게 필요 이상으로 많은 권한을 부여하게 될 수 있습니다. Hello 먼저에서 하면 안 되는 일부 사용자가 액세스 toodata 함으로써 toodata 손상이 발생할 수 있습니다.

toolearn RBAC에 대 한 내용은 참조 하십시오.

- [Azure 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)
- [Azure 역할 기반 액세스 제어의 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md)
- [Azure 저장소 보안 가이드](../storage/common/storage-security-guide.md) 어떻게 toosecure 저장소 계정과 RBAC에 대 한 내용은

## <a name="storage-encryption"></a>저장소 암호화
### <a name="use-client-side-encryption-for-high-value-data"></a>고가치 데이터에 대해 클라이언트 쪽 암호화 사용

클라이언트 쪽 암호화 있습니다 tooprogrammatically tooAzure 저장소에 업로드 하기 전에 전송 되는 데이터를 암호화 하 고 프로그래밍 방식으로 저장소에서 검색할 때 데이터를 해독할 수 있습니다.  이를 통해 전송 중인 데이터와 미사용 데이터를 모두 암호화할 수 있습니다.  클라이언트 쪽 암호화 란 데이터를 암호화 하면의 hello 가장 안전한 방법 하지만 toomake 프로그래밍 방식으로 변경 내용을 tooyour 응용 프로그램 해야 않으며 제 자리에 키 관리 프로세스를 배치 합니다.

클라이언트 쪽 암호화, 암호화 키에 대 한 유일한 제어 toohave 사용 합니다.  자체 암호화 키를 생성하고 관리할 수 있습니다.  클라이언트 쪽 암호화 여기서 hello Azure 저장소 클라이언트 라이브러리에서는 오류가 발생 하는 콘텐츠 암호화 키 (CEK) 래핑된 다음 hello 키 암호화 키 KEK ()를 사용 하 여 (암호화)는 봉투 (envelope) 기술을 사용 합니다. hello KEK 키 식별자로 식별 되는 비대칭 키 쌍 또는 대칭 키 및 수 하거나 수 있습니다 로컬로 관리에 저장 된 [Azure 키 자격 증명 모음](../key-vault/key-vault-whatis.md)합니다.

클라이언트 쪽 암호화 변환은 hello Java와 hello.NET 저장소 클라이언트 라이브러리에 있습니다.  클라이언트 응용 프로그램 내에서 데이터를 암호화하고 자체 암호화 키를 생성 및 관리하는 방법에 대한 자세한 내용은 [Microsoft Azure 저장소용 클라이언트 쪽 암호화 및 Azure Key Vault](../storage/storage-client-side-encryption.md)를 참조하세요.

### <a name="azure-disk-encryption-for-vms"></a>VM에 대한 Azure Disk Encryption
Azure Disk Encryption은 Windows 및 Linux IaaS 가상 컴퓨터 디스크를 암호화할 수 있도록 하는 기능입니다. Azure 디스크 암호화는 windows hello 업계 표준 BitLocker 기능 및 운영 체제 hello에 대 한 Linux tooprovide 볼륨 암호화의 hello DM 암호화 기능 및 hello 데이터 디스크를 활용합니다. hello 솔루션은 Azure 키 자격 증명 모음 toohelp 제어 하 고 주요 자격 증명 모음 구독에서 hello 디스크 암호화 키 및 암호를 관리할와 통합 됩니다. hello 솔루션 하면 hello 가상 컴퓨터 디스크에 있는 모든 데이터가 Azure 저장소에 저장 된 상태의 암호화 됩니다.

[Windows 및 Linux IaaS VM용 Azure Disk Encryption](azure-security-disk-encryption.md)을 참조하세요.

### <a name="storage-service-encryption"></a>저장소 서비스 암호화
때 [저장소 서비스 암호화](../storage/storage-service-encryption.md) aes-256 암호화를 사용 하 여 자동으로 hello 데이터는 암호화에 파일 저장을 사용 합니다. Microsoft는 모든 hello 암호화, 해독 및 키 관리를 처리합니다. 이 기능은 LRS 및 GRS 중복 유형에 사용할 수 있습니다.

## <a name="next-steps"></a>다음 단계
이 문서에서는 PaaS 웹 및 모바일 응용 프로그램 보안에 대 한 보안 모범 사례 Azure 저장소의 tooa 컬렉션을 도입 되었습니다. PaaS 배포의 경우 보안에 대 한 더 toolearn 참조:

- [PaaS 배포 보안](security-paas-deployments.md)
- [Azure App Services를 사용하여 PaaS 웹 및 모바일 응용 프로그램 보안](security-paas-applications-using-app-services.md)
- [Azure에서 PaaS 데이터베이스 보안 유지](security-paas-applications-using-sql.md)
