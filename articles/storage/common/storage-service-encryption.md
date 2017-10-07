---
title: "미사용 데이터에 대 한 저장소 서비스 암호화 aaaAzure | Microsoft Docs"
description: "사용 하 여 hello Azure 저장소 서비스 암호화 기능 tooencrypt Azure Blob 저장소 서비스 쪽 hello hello 데이터를 저장할 때 및 hello 데이터를 검색할 때 암호를 해독 합니다."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: edabe3ee-688b-41e0-b34f-613ac9c3fdfd
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: robinsh
ms.openlocfilehash: 4e03c5704071281a798936d41d86456afcfdec77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-service-encryption-for-data-at-rest"></a>휴지 상태의 데이터에 대한 Azure 저장소 서비스 암호화
Azure 저장소 서비스 암호화 SSE ()을 미사용 데이터를 사용 하면 조직의 보안 및 규정 준수 약정 데이터 toomeet를 보호 하 고 보호 합니다. 이 기능을 Azure 저장소는 자동으로 데이터 사전 toopersisting toostorage를 암호화 하 고 이전 tooretrieval 해독 합니다. hello 암호화, 해독 및 키 관리에 완전히 투명 한 toousers 됩니다.

hello 다음 섹션에서는 자세한 지침을 제공 hello 뿐만 아니라 toouse hello 저장소 서비스 암호화 기능 시나리오 및 사용자 환경을 원하는 하는 방법에 있습니다.

## <a name="overview"></a>개요
Azure 저장소는 다양 한 개발자를 함께 사용 하는 보안 기능 toobuild 보안 응용 프로그램을 제공 합니다. [클라이언트 쪽 암호화](../storage-client-side-encryption.md), HTTP 또는 SMB 3.0을 사용하여 응용 프로그램과 Azure 간에 전송 중인 데이터의 보안을 유지할 수 있습니다. 저장소 서비스 암호화는 휴지 상태의 암호화를 제공하며 암호화, 암호 해독, 키 관리를 완전히 투명한 방식으로 처리합니다. 256 비트를 사용 하 여 모든 데이터는 암호화 [AES 암호화](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), 사용할 수 있는 암호 hello 가장 강력한 블록 중 하나입니다.

SSE는 tooAzure 저장소, 작성 하 고 Azure Blob 저장소 및 파일 저장소에 사용할 수 있습니다 때 hello 데이터를 암호화 하 여 작동 합니다. Hello 다음에 대 한 작동 합니다.

* 표준 저장소: Blob에 대한 범용 저장소 계정과 File Storage 및 Blob Storage 계정
* Premium Storage 
* 모든 중복 수준(LRS, ZRS, GRS, RA-GRS)
* Azure Resource Manager 저장소 계정(클래식 아님) 
* 모든 지역

toolearn을 참조 하십시오 toohello FAQ.

저장소 계정에 대 한 저장소 서비스 암호화 hello에 로그인 할 tooenable 또는 사용 안 함 [Azure 포털](https://portal.azure.com) 하 고 저장소 계정을 선택 합니다. Hello 설정 블레이드에서이 스크린샷에 표시 된 대로 Blob 서비스 섹션 hello에 대 한 확인 하 고 암호화를 클릭 합니다.

![암호화 옵션을 보여 주는 포털 스크린샷](./media/storage-service-encryption/image1.png)
<br/>*그림 1: Blob Service에 SSE 사용(1단계)*

![암호화 옵션을 보여 주는 포털 스크린샷](./media/storage-service-encryption/image3.png)
<br/>*그림 2: 파일 서비스에 SSE 사용(1단계)*

Hello 암호화 설정을 클릭 한 후 사용 하도록 설정 하거나 저장소 서비스 암호화를 사용 하지 않도록 설정할 수 있습니다.

![암호화 속성을 보여 주는 포털 스크린샷](./media/storage-service-encryption/image2.png)
<br/>*그림 3: Blob 및 파일 서비스에 SSE 사용(2단계)*

## <a name="encryption-scenarios"></a>암호화 시나리오
저장소 계정 수준에서 저장소 서비스 암호화를 사용할 수 있습니다. 활성화 되 면 어떤 서비스 tooencrypt 고객을 선택 합니다. Hello 다음 고객 시나리오를 지원 합니다.

* 리소스 관리자 계정의 Blob Storage 및 File Storage 암호화
* Blob 및 파일 서비스의에서 암호화 클래식 저장소 계정 한 번 tooResource Manager 저장소 계정 마이그레이션.

SSE 다음과 같은 제한을 hello에 있습니다.

* 클래식 저장소 계정의 암호화는 지원되지 않습니다.
* 기존 데이터 요금-SSE hello 암호화가 사용 하도록 설정만 새로 만든된 데이터를 암호화 합니다. 예를 들어 새 리소스 관리자 저장소 계정을 만드는 하지만 암호화를 사용 하지 않는 한 blob 또는 보관 된 Vhd toothat 저장소 계정에 업로드 하 고 다음 SSE 설정 하는 다음 경우 다시 작성 하거나 복사 하는 경우가 아니면 해당 blob 암호화 되지 않습니다.
* 마켓플레이스 지원-Enable Vm의 암호화에서 만든 hello hello를 사용 하 여 마켓플레이스 [Azure 포털](https://portal.azure.com), PowerShell 및 Azure CLI 합니다. hello VHD에 대 한 기본 이미지; 암호화 되지 않은 상태로 유지 됩니다. 그러나 VM hello가 생성 한 후에 수행 된 쓰기 암호화 됩니다.
* 테이블 및 큐 데이터는 암호화되지 않습니다.

## <a name="getting-started"></a>시작하기
### <a name="step-1-create-a-new-storage-accountstorage-create-storage-accountmd"></a>1단계: [새 저장소 계정 만들기](../storage-create-storage-account.md).
### <a name="step-2-enable-encryption"></a>2단계: 암호화 사용.
Hello를 사용 하 여 암호화를 사용 하도록 설정할 수 [Azure 포털](https://portal.azure.com)합니다.

> [!NOTE]
> Hello tooprogrammatically 사용 하려면 저장소 계정에서 저장소 서비스 암호화 hello를 사용 하지 않도록 설정 하거나, 사용할 수 있습니다 [Azure 저장소 리소스 공급자 REST API](https://msdn.microsoft.com/library/azure/mt163683.aspx), hello [저장소 리소스 공급자 클라이언트 라이브러리 .NET 용](https://msdn.microsoft.com/library/azure/mt131037.aspx), [Azure PowerShell](/powershell/azureps-cmdlets-docs), 또는 hello [Azure CLI](../storage-azure-cli.md)합니다.
> 
> 

### <a name="step-3-copy-data-toostorage-account"></a>3 단계: 데이터 toostorage 계정 복사
Hello Blob 서비스에 대 한 SSE를 사용 하면, toothat 저장소 계정 작성 된 모든 blob이 암호화 됩니다. 저장소 계정에 이미 있는 모든 Blob는 다시 작성할 때까지 암호화되지 않습니다. 암호화, SSE와 한 저장소 계정 tooone에서 hello 데이터를 복사 또는 SSE를에서 이전 데이터 암호화 되어 하나의 컨테이너 tooanother toosure hello blob을 복사 합니다. 사용할 수 있습니다 hello 도구 tooaccomplish 다음 중 하나입니다. 파일 저장소에도 동일한 동작을 hello는이 합니다.

#### <a name="using-azcopy"></a>AzCopy 사용
AzCopy는 간단한 명령을 사용 하 여 최적의 성능으로 Microsoft Azure Blob, 파일 및 테이블 저장소에서 데이터 tooand 복사를 위해 설계 된 Windows 명령줄 유틸리티입니다. 이 toocopy blob 또는 SSE 사용 하도록 설정 된 하나의 저장소 계정 tooanother에서 파일에 사용할 수 있습니다. 

toolearn을 방문 하세요 [hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송](storage-use-azcopy.md)합니다.

#### <a name="using-smb"></a>SMB 사용
Azure 파일 저장소 hello 표준 SMB 프로토콜을 사용 하 여 hello 클라우드에서 파일 공유를 제공 합니다. 온-프레미스 또는 Azure의 클라이언트에서 파일 공유를 마운트할 수 있습니다. 탑재 면 Robocopy와 같은 도구 tooAzure 파일 공유를 통해 사용된 toocopy 파일 일 수 있습니다. 자세한 내용은 참조 [toomount Azure 파일 공유 어떻게 Windows에서](../files/storage-how-to-use-files-windows.md) 및 [linux toomount Azure 파일을 공유 하는 방법](../storage-how-to-use-files-linux.md)합니다.


#### <a name="using-hello-storage-client-libraries"></a>Hello 저장소 클라이언트 라이브러리를 사용 하 여
Blob 저장소에서 또는 다양 한.NET, c + +, Java, Android, Node.js, PHP, Python 및 Ruby를 비롯 한 저장소 클라이언트 라이브러리를 사용 하 여 저장소 계정 간에 blob 또는 파일 데이터 tooand를 복사할 수 있습니다.

toolearn을 방문 하세요 우리의 [.NET을 사용 하 여 Azure Blob 저장소 시작](../blobs/storage-dotnet-how-to-use-blobs.md)합니다.

#### <a name="using-a-storage-explorer"></a>저장소 탐색기 사용
하면 저장소 탐색기 toocreate 저장소 계정을 사용 하 여, 업로드 및 데이터 다운로드, blob의 내용을 보는 및 디렉터리를 통해 이동 합니다. 암호화가 설정 되어 이러한 tooupload blob tooyour 저장소 계정 중 하나를 사용할 수 있습니다. 일부 저장소 탐색기와 SSE를 사용할 수 있는 새 저장소 계정 또는 기존 blob 저장소 tooa 다른 컨테이너에서 hello 저장소 계정에서 데이터를 복사할 수도 있습니다.

toolearn을 방문 하세요 [Azure 저장소 탐색기](../storage-explorers.md)합니다.

### <a name="step-4-query-hello-status-of-hello-encrypted-data"></a>4 단계: hello hello 상태 쿼리 암호화 된 데이터
수 있는 개체 toodetermine의 tooquery hello 상태 또는 암호화 되어 있으면 업데이트 된 버전의 hello 저장소 클라이언트 라이브러리 배포 되었습니다. 현재 Blob 저장소에만 사용할 수 있습니다. 파일 저장소에 대 한 지원 hello 로드맵 켜져 있습니다. 

Hello 그 동안 호출할 수 있습니다 [계정 속성 가져오기](https://msdn.microsoft.com/library/azure/mt163553.aspx) 저장소 계정 hello tooverify에 암호화 사용 또는 hello hello Azure 포털에서에서 저장소 계정 속성 보기.

## <a name="encryption-and-decryption-workflow"></a>암호화 및 암호 해독 워크플로
암호화/암호 해독 워크플로 hello에 대 한 간단한 설명은 다음과 같습니다.

* hello 고객 hello 저장소 계정에서 암호화를 설정 합니다.
* 새 데이터 (예: PUT Blob, 배치 블록, PUT Page, 배치 파일 등) tooBlob 또는 파일 저장소; hello 고객 기록 하는 경우 모든 쓰기 256 비트를 사용 하 여 암호화 되어 [AES 암호화](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), 사용할 수 있는 암호 hello 가장 강력한 블록 중 하나입니다.
* Hello 고객이 tooaccess 데이터 (Blob 가져오기, 등), toohello 사용자를 반환 하기 전에 데이터는 자동으로 해독 합니다.
* 암호화를 해제 하는 경우 새로운 쓰기는 더 이상 암호화 되며 기존의 암호화 된 데이터 암호화 상태를 유지 hello 사용자가 다시 작성 합니다. 암호화를 사용 하는 동안 tooBlob 또는 파일 저장소를 암호화할 씁니다. hello 저장소 계정에 대 한 암호화를 활성화/비활성화을 전환 하는 hello 사용자와 데이터의 hello 상태 변경 되지 않습니다.
* 모든 암호화 키는 Microsoft에서 저장, 암호화 및 관리합니다.

## <a name="frequently-asked-questions-about-storage-service-encryption-for-data-at-rest"></a>미사용 데이터에 대한 저장소 서비스 암호화에 대한 질문과 대답
**Q: 기존 클래식 저장소 계정이 있습니다. 이 계정에 SSE를 사용할 수 있나요?**

A: 아니요, SSE는 Resource Manager 저장소 계정에만 지원됩니다.

**Q: 내 클래식 저장소 계정에서 데이터를 암호화하려면 어떻게 해야 하나요?**

A: 새 저장소 계정 리소스 관리자를 만들고 사용 하 여 데이터를 복사할 수 있습니다 [AzCopy](storage-use-azcopy.md) 기존 클래식 저장소 계정에서 tooyour 새로 만든 저장소 계정 리소스 관리자입니다. 

클래식 저장소 계정을 tooa 저장소 계정 리소스 관리자를 마이그레이션하는 경우이 작업은 즉각적인를 사용자의 계정 유형을 hello 변경 되지만 기존 데이터는 영향을 주지 않습니다. 새로 기록되는 데이터는 암호화를 사용하도록 설정한 후에만 암호화됩니다. 자세한 내용은 참조 [플랫폼 지원 마이그레이션의 IaaS에서에서 리소스 관리자 클래식 tooResource](https://azure.microsoft.com/blog/iaas-migration-classic-resource-manager/)합니다. 이 기능은 Blob 및 파일 서비스에 대해서만 지원됩니다.

**Q: 기존의 Resource Manager 저장소 계정이 있습니다. 이 계정에 SSE를 사용할 수 있나요?**

A: 예, 하지만 새로 작성한 데이터만 암호화됩니다. 돌아가 기존에 있는 데이터를 암호화하지 않습니다. 이 아직 지원 되지 않습니다 hello 파일 저장소 미리 보기에 대 한 합니다.

**Q: 기존 저장소 계정 리소스 관리자의에서 현재 데이터 hello를 tooencrypt 겠어요?**

A: Resource Manager 저장소 계정에서 언제든지 SSE를 사용하도록 설정할 수 있습니다. 그러나 이미 있던 데이터는 암호화되지 않습니다. 기존 데이터 용량의 tooencrypt tooanother 이름이 나 다른 컨테이너를 복사 하 고 다음 hello 암호화 되지 않은 버전을 제거할 수 있습니다.

**Q: 프리미엄 저장소를 사용 중입니다. SSE를 사용할 수 있나요?**

A: 예, SSE는 표준 저장소 및 프리미엄 저장소 모두에서 지원됩니다.  프리미엄 저장소 hello 파일 서비스에 대 한 지원 되지 않습니다.

**Q: 새 저장소 계정을 만들고 SSE를 사용한 경우 이 저장소 계정을 사용하여 새 VM을 만들면 내 VM이 암호화되어 있나요?**

A: 예. SSE 사용 하도록 설정한 후 사용자에 게 만들어질으로 만든 hello 새 저장소 계정을 사용 하는 모든 디스크 암호화 됩니다. VM을 Azure Market Place hello VHD에 대 한 기본 이미지를 사용 하 여 만들어진 hello; 암호화 되지 않은 상태로 유지 되 면 그러나 VM hello가 생성 한 후에 수행 된 쓰기 암호화 됩니다.

**Q: Azure PowerShell 및 Azure CLI를 사용하여 SSE가 사용된 새 저장소 계정을 만들 수 있나요?**

A: 예.

**Q: SSE를 사용하는 경우 Azure 저장소 비용은 얼마나 늘어나나요?**

A: 추가 비용은 없습니다.

**Q: 누구 hello 암호화 키를 관리?**

A: hello 키 Microsoft에서 관리 됩니다.

**Q: 나만의 암호화 키를 사용할 수 있나요?**

A: 제작 하는 암호화 키가 자신의 고객 toobring에 기능을 제공 합니다.

**Q: 액세스 toohello 암호화 키 취소 수 있습니까?**

A: 현재는 없습니다. hello 키 Microsoft에서 완전히 관리 됩니다.

**Q: 새 저장소 계정을 만들 때 기본적으로 SSE가 사용되도록 설정되어 있나요?**

A: SSE 기본적으로 사용 되지 않습니다. Azure 포털 tooenable hello를 사용할 수 있습니다 것입니다. 또한 프로그래밍 방식으로 hello 저장소 리소스 공급자 REST API를 사용 하 여이 기능을 사용할 수 있습니다.

**Q: Azure Disk Encryption과 어떻게 다른가요?**

A:가 기능은 Azure Blob 저장소에 사용 되는 tooencrypt 데이터에 설명 합니다. hello Azure 디스크 암호화는 IaaS Vm의 OS 및 데이터 디스크를 사용 하는 tooencrypt 합니다. 자세한 내용은 [저장소 보안 가이드](../storage-security-guide.md)를 참조하세요.

**Q: 어떻게 하면 SSE 및 다음에서 설정 및 hello 디스크에서 Azure 디스크 암호화를 사용 하도록 설정?**

A: 이것은 원활하게 작동합니다. 데이터는 두 가지 방법으로 암호화됩니다.

**Q: 내 저장소 계정이 지리적 중복 복제 toobe 설정 되어 있습니다. SSE를 사용하도록 설정하는 경우 내 중복 복사본도 암호화되나요?**

A: 예, hello 저장소 계정의 모든 복사본을 암호화 하 고 – 로컬 중복 저장소 (LRS), 영역 중복 저장소 (ZRS), 지역 중복 저장소 (GRS) 및 읽기 액세스 지역 중복 저장소 (RA-GRS) – 모든 중복 옵션이 지원 됩니다.

**Q: 내 저장소 계정에서 암호화를 사용할 수 없습니다.**

A: Resource Manager 저장소 계정인가요? 클래식 저장소 계정은 지원되지 않습니다. 

**Q: SSE는 특정 지역에만 허용되나요?**

A: hello SSE은 Blob 저장소에 대 한 모든 지역에서 사용할 수 있습니다. 파일 저장소의 가용성 섹션 hello를 확인 하십시오. 

**Q: 어떻게에 게 문의 합니까 누군가가 tooprovide 피드백 또는 문제가 발생 합니까?**

A:에 게 문의 하십시오 [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) tooStorage 서비스 암호화 관련 된 문제에 대 한 합니다.

## <a name="next-steps"></a>다음 단계
Azure 저장소는 다양 한 개발자를 함께 사용 하는 보안 기능 toobuild 보안 응용 프로그램을 제공 합니다. 자세한 내용은 방문 hello [저장소 보안 가이드](../storage-security-guide.md)합니다.

