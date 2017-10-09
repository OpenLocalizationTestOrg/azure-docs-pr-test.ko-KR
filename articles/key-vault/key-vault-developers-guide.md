---
title: "aaaAzure 키 자격 증명 모음 개발자 가이드"
description: "개발자는 Azure 키 자격 증명 모음 toomanage hello Microsoft Azure 환경 내에서 암호화 키를 사용할 수 있습니다."
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: 631cea1315964cd0b97e8b2cf3311754230fb801
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-developers-guide"></a>Azure Key Vault 개발자 가이드

주요 자격 증명 모음 toosecurely 액세스 중요 한 정보를를 응용 프로그램 내에서 있습니다.

- 키와 암호를 직접 toowrite hello 코드 필요 없이 보호 기능을 쉽게 수 toouse는 응용 프로그램에서 합니다.
- 고유 고객 수 toohave은 및 hello 핵심 소프트웨어 기능을 제공 하에 집중할 수 있도록 자체 키를 관리 합니다. 이러한 방식으로 응용 프로그램 hello 책임이 나 고객의 테 넌 트 키 및 암호에 대 한 잠재적인 책임 소유 하지 않습니다.
- 응용 프로그램 서명 키를 사용할 수 없으며 아직 암호화 키 관리 hello 솔루션 toobe 지리적으로 분산 된 응용 프로그램으로 적합 한 수 있도록 응용 프로그램에서 외부 있습니다.
- 응용 프로그램은 hello 2016 년 9 월 릴리스를 기준으로 키 자격 증명 모음 키 자격 증명 모음을 사용 이제 수 [인증서](https://docs.microsoft.com/rest/api/keyvault/certificate-operations)합니다. 자세한 내용은 [키, 암호 및 인증서 정보](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates)를 참조하세요.

Azure Key Vault에 대한 일반적인 내용은 [키 자격 증명 모음이란?](key-vault-whatis.md)을 참조하세요.

## <a name="public-previews"></a>공개 미리 보기

새로운 Key Vault 기능의 공개 미리 보기가 정기적으로 릴리스됩니다. 이러한 공개 미리 보기를 사용해보고, 피드백 메일 주소인 azurekeyvault@microsoft.com을 통해 의견을 알려주세요.

### <a name="storage-account-keys---july-10-2017"></a>저장소 계정 키 - 2017년 7월 10일

>[!NOTE]
>이 업데이트의 유일한 hello Azure 키 자격 증명 모음에 대 한 **저장소 계정 키** 기능은 미리 보기에서 제공 됩니다.

이 미리 보기에는 [.NET/C#](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault/), [REST](https://docs.microsoft.com/rest/api/keyvault/) 및 [PowerShell](https://docs.microsoft.com/powershell/module/azurerm.keyvault/) 인터페이스를 통해 사용할 수 있는 새로운 저장소 계정 키가 포함되어 있습니다. 

새 저장소 계정 키 기능 hello에 대 한 자세한 내용은 참조 하십시오. [Azure 키 자격 증명 모음 저장소 계정 키 개요](key-vault-ovw-storage-keys.md)합니다.

## <a name="videos"></a>비디오

이 동영상에서는 toocreate 고유한 키 자격 증명 모음 방법 등에 toouse hello ' Hello 키 자격 증명 모음 ' 샘플 응용 프로그램에서 합니다.

- [Key Vault 개발자 - 빠른 시작 가이드](https://channel9.msdn.com/Blogs/Azure/Azure-Key-Vault-Developer-Quick-Start/player)

위 비디오에 언급된 리소스:

- [Azure PowerShell](http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409)
- [Azure Key Vault 샘플 코드](http://go.microsoft.com/fwlink/?LinkId=521527&clcid=0x409)

## <a name="creating-and-managing-key-vaults"></a>주요 자격 증명 모음 만들기 및 관리

코드에서 Azure 키 자격 증명 모음과 작업을 하기 전에 생성 하 고 hello 다음 문서에에서 설명 된 대로 REST, 리소스 관리자 템플릿, PowerShell 또는 CLI를 통해 자격 증명 모음을 관리 수 있습니다.:

- [REST를 사용하여 주요 자격 증명 모음 만들기 및 관리](https://docs.microsoft.com/rest/api/keyvault/)
- [PowerShell을 사용하여 키 자격 증명 모음 만들기 및 관리](key-vault-get-started.md)
- [CLI를 사용하여 키 자격 증명 모음 만들기 및 관리](key-vault-manage-with-cli2.md)
- [Azure Resource Manager 템플릿을 통한 Key Vault 만들기 및 암호 추가](../azure-resource-manager/resource-manager-template-keyvault.md)

> [!NOTE]
> 주요 자격 증명 모음에 대한 작업은 AAD를 통해 인증되고 자격 증명 모음당 정의되는 주요 자격 증명 모음의 액세스 정책을 통해 권한이 부여됩니다.

## <a name="coding-with-key-vault"></a>주요 자격 증명 모음을 사용한 코딩

hello 프로그래머를 위한 주요 자격 증명 모음 관리 시스템 여러 인터페이스를 rest hello 기반으로 구성 됩니다. Hello REST 인터페이스를 통해 키 자격 증명 모음 리소스 모두에 액세스할 수 있음 키, 암호 및 인증서를 선택 합니다. [Key Vault REST API 참조](https://docs.microsoft.com/rest/api/keyvault/). 

### <a name="supported-programming-languages"></a>지원되는 프로그래밍 언어

#### <a name="net"></a>.NET

- [Key Vault에 대한 .NET API 참조](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault) 

Hello 2.x 버전의.NET SDK hello에 대 한 자세한 내용은 참조 hello [릴리스 정보](key-vault-dotnet2api-release-notes.md)합니다.

#### <a name="java"></a>Java

- [Key Vault용 Java SDK](https://docs.microsoft.com/java/api/com.microsoft.azure.keyvault)

#### <a name="nodejs"></a>Node.js

Node.js에서 hello 자격 증명 모음 관리 API 및 hello 자격 증명 모음 개체 API 구분 됩니다. Key Vault 관리를 사용하면 주요 자격 증명 모음을 만들고 업데이트할 수 있습니다. Key Vault 운영 API는 키, 암호, 인증서 등의 자격 증명 모음 개체 작업에 사용됩니다. 

- [Key Vault 관리에 대한 Node.js API 참조](http://azure.github.io/azure-sdk-for-node/azure-arm-keyvault/latest/)
- [Key Vault 작업에 대한 Node.js API 참조](http://azure.github.io/azure-sdk-for-node/azure-keyvault/latest/) 

### <a name="quick-start"></a>빠른 시작

- [주요 자격 증명 모음 만들기](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
- [Node.js에서 Key Vault 시작](https://azure.microsoft.com/en-us/resources/samples/key-vault-node-getting-started/)

### <a name="code-examples"></a>코드 예제

응용 프로그램에서 Key Vault를 사용하는 전체 예제는 다음을 참조하세요.

- [Azure Key Vault 코드 샘플](http://www.microsoft.com/download/details.aspx?id=45343) - .NET 샘플 응용 프로그램 *HelloKeyVault* 및 Azure 웹 서비스 예제입니다. 
- [웹 응용 프로그램에서 Azure 키 자격 증명 모음을 사용 하 여](key-vault-use-from-web-application.md) -자습서 toohelp 어떻게 toouse Azure 키 자격 증명 모음에 있는 웹 응용 프로그램을 Azure에 알아봅니다. 

## <a name="how-tos"></a>방법

hello 문서 आ स ा 시나리오 제공 Azure 키 자격 증명 모음을 사용 하기 위한 작업 관련 지침:

- [구독 한 후 변경 주요 자격 증명 모음 테 넌 트 ID 이동](key-vault-subscription-move-fix.md) -tootenant B 테 넌 트의 Azure 구독을 이동, 사용자 기존 키 자격 증명 모음이 B. 수정이이 가이드를 사용 하 여이 테 넌 트의 hello 이름 (사용자 및 응용 프로그램)에 액세스할 수 없는 합니다.
- [방화벽 뒤에 있는 주요 자격 증명 모음에 액세스](key-vault-access-behind-firewall.md) -tooaccess 키 자격 증명 모음에 키 자격 증명 모음 클라이언트 응용 프로그램 요구 toobe 수 tooaccess에 다양 한 기능에 대 한 여러 끝점입니다.
- [어떻게 tooGenerate 및 Azure 키 자격 증명 모음에 대 한 Transfer HSM-Protected 키](key-vault-hsm-protected-keys.md) -이렇게 하면 계획을 생성 하 고 다음 사용자 고유의 HSM 보호 키 toouse Azure 키 자격 증명을 전송 합니다.
- [어떻게 toopass 값 (예: 암호)을 배포 하는 동안 보안](../azure-resource-manager/resource-manager-keyvault-parameter.md) -배포 중 매개 변수로 toopass를 안전한 값 (예: 암호)를 해야 하는 경우는 다른 Azure 키 자격 증명 모음 및 참조 hello 값에서으로 해당 값을 저장할 수 있습니다 리소스 관리자 템플릿을 합니다.
- [어떻게 toouse 키 자격 증명 모음 SQL Server와 확장 가능 키 관리에 대 한](https://msdn.microsoft.com/library/dn198405.aspx) -Azure 키 자격 증명 모음을 사용 하면 관리 EKM (Extensible Key) 공급자와 SQL Server 및 SQL--a-VM에서 tooleverage hello Azure 키 자격 증명 모음 서비스에 대 한 SQL Server 커넥터를 hello 응용 프로그램 링크;에 대 한 tooprotect 암호화 키 투명 한 데이터 암호화, 백업 암호화 및 열 수준 암호화 합니다.
- [어떻게 키 자격 증명 모음에서 toodeploy 인증서 tooVMs](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/) -VM에서 실행 되는 Azure 요구 사항에는 인증서는 클라우드 응용 프로그램입니다. 지금 이 VM으로 인증서를 가져오려면 어떻게 하나요?
- [최종 tooend 키 자격 증명 모음을 tooset 키 회전 및 감사 어떻게](key-vault-key-rotation-log-monitoring.md) -이 예제는 다음 방법을 통해 tooset 키 회전 및 Azure 키 자격 증명 감사 합니다.
- [Key Vault를 통한 Azure Web App Certificate 배포]( https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)는 [App Service Certificate](https://azure.microsoft.com/blog/internals-of-app-service-certificate/) 제품의 일부로 Key Vault에 저장된 인증서를 배포하기 위한 단계별 지침을 제공합니다.
- [주요 자격 증명 모음 사용 권한을 toomany 응용 프로그램 tooaccess 부여](key-vault-group-permissions-for-apps.md) 주요 자격 증명 모음 액세스 제어 정책만 16 항목을 지원 합니다. 그러나 Azure Active Directory 보안 그룹을 만들 수 있습니다. 모든 hello 연결 서비스 보안 주체 toothis 보안 그룹 및 다음 액세스 toothis 보안 그룹 tooKey 자격 증명 모음을 부여를 추가 합니다.
- Azure에서 Key Vault를 통합 및 사용하는 방법에 대한 작업별 지침은 [Key Vault에 대한 Ryan Jones Azure Resource Manager 템플릿 예제](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples)를 참조하세요.
- [CLI 키 자격 증명 모음 toouse 소프트-삭제 방법을](key-vault-soft-delete-cli.md) 소프트 삭제 사용 하도록 설정 된 hello 사용 및 주요 자격 증명 모음 및 다양 한 키 자격 증명 모음 개체의 수명 주기를 통해 안내 합니다.
- [PowerShell과 함께 키 자격 증명 모음 toouse 소프트-삭제 방법을](key-vault-soft-delete-powershell.md) 소프트 삭제 사용 하도록 설정 된 hello 사용 및 주요 자격 증명 모음 및 다양 한 키 자격 증명 모음 개체의 수명 주기를 통해 안내 합니다.

## <a name="integrated-with-key-vault"></a>주요 자격 증명 모음과 통합됨

다음 문서에서는 사용하거나 Key Vault와 통합하는 다른 시나리오 및 서비스에 대한 정보를 다룹니다.

- [Azure 디스크 암호화](../security/azure-security-disk-encryption.md) 활용 하 여 hello 업계 표준 [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) 창과 hello의 기능 [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) hello OS 및 hello 데이터에 대 한 Linux tooprovide 볼륨 암호화의 기능 디스크가 필요 합니다. hello 솔루션은 Azure 키 자격 증명 모음 toohelp 제어 하 고 주요 자격 증명 모음 구독에서 Azure 저장소의 hello 가상 컴퓨터 디스크에서 모든 데이터가 암호화 되는 동시에 hello 디스크 암호화 키 및 암호를 관리할와 통합 됩니다.
- [Azure 데이터 레이크 저장소](../data-lake-store/data-lake-store-get-started-portal.md) hello 계정에 저장 된 데이터의 암호화에 대 한 옵션을 제공 합니다. 데이터 레이크 저장소 키 관리에 대 한 hello Data Lake 저장소에에서 저장 된 모든 데이터를 암호 해독에 필요한 마스터 암호화 키 (MEKs)을 관리 하기 위한 두 가지 모드를 제공 합니다. 데이터 레이크 저장소 hello MEKs를 관리 하거나 tooretain 소유권 hello MEKs 계정을 사용 하 여 Azure 키 자격 증명 모음을 선택 하거나 하도록 할 수 있습니다. 데이터 레이크 저장소 계정을 만드는 동안 키 관리 hello 모드를 지정 합니다. 
- [Azure Information Protection](/information-protection/plan-design/plan-implement-tenant-key) toomanager 사용 하면 테 넌 트 키입니다. 예를 들어 Microsoft를 테 넌 트 키 (hello 기본값)을 관리 하는 대신 직접 테 넌 트 키 toocomply tooyour 조직에 적용 되는 특정 규정을 관리할 수 있습니다. 테 넌 트 키 관리 이기도 고유한 키 또는 BYOK 참조 tooas 상태로 전환 합니다.

## <a name="key-vault-overviews-and-concepts"></a>Key Vault 개요 및 개념

- [주요 자격 증명 모음 소프트 삭제 동작이](key-vault-ovw-soft-delete.md) 여부에 관계 없이 hello 삭제 실수로 또는 의도적으로 삭제 된 개체를 복구할 수 있도록 하는 기능에 설명 합니다.
- [주요 자격 증명 모음 클라이언트 제한](key-vault-ovw-throttling.md) 제한의 기본 개념 toohello 방향이 설정 및 앱에 대 한는 접근 방식을 제공 합니다.
- [주요 자격 증명 모음 저장소 계정 키 개요](key-vault-ovw-storage-keys.md) hello 주요 자격 증명 모음 통합 Azure 저장소 계정 키에 설명 합니다.
- [주요 자격 증명 모음 보안 권역](key-vault-ovw-security-worlds.md) 지역과 보안 영역 사이의 hello 관계에 설명 합니다.

## <a name="social"></a>사회적

- [키 자격 증명 모음 블로그](http://aka.ms/kvblog)
- [키 자격 증명 모음 포럼](http://aka.ms/kvforum)

## <a name="supporting-libraries"></a>라이브러리 지원

- [Microsoft Azure Key Vault 핵심 라이브러리](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Core)는 식별자의 키를 찾고 키로 작업을 수행하기 위한 **IKey** 및 **IKeyResolver** 인터페이스를 제공합니다.
- [Microsoft Azure Key Vault 확장](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Extensions)은 Azure Key Vault에 확장된 기능을 제공합니다.


