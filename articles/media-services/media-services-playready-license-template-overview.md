---
title: "aaaMedia 서비스 PlayReady 라이선스 템플릿 개요"
description: "이 항목에서는 tooconfigure PlayReady 라이선스 사용 되는 PlayReady 라이선스 템플릿 개요를 제공 합니다."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: fddce5d0-1278-478f-ae05-9b985c748731
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 5a5ba930c56f70038db204681486ebc4308199fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-playready-license-template-overview"></a><span data-ttu-id="88771-103">Media Services PlayReady 라이선스 템플릿 개요</span><span class="sxs-lookup"><span data-stu-id="88771-103">Media Services PlayReady license template overview</span></span>
<span data-ttu-id="88771-104">Azure 미디어 서비스는 현재 Microsoft PlayReady 라이선스를 배달하는 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="88771-104">Azure Media Services now provides a service for delivering Microsoft PlayReady licenses.</span></span> <span data-ttu-id="88771-105">Hello 최종 사용자 플레이어 (예: Silverlight) tooplay 하려고 할 때 PlayReady 보호 된 콘텐츠, 보낸된 toohello 라이선스 배달 서비스 tooobtain 라이선스를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="88771-105">When hello end user player (for example, Silverlight) tries tooplay your PlayReady protected content, a request is sent toohello license delivery service tooobtain a license.</span></span> <span data-ttu-id="88771-106">Hello 라이선스 서비스 hello 요청을 승인 하는 경우 보낸된 toohello 클라이언트 중인 hello 라이선스를 발급 하 고 수 수 사용된 toodecrypt 앤 플레이 hello 지정 된 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="88771-106">If hello license service approves hello request, it issues hello license which is sent toohello client and can be used toodecrypt and play hello specified content.</span></span>

<span data-ttu-id="88771-107">또한 미디어 서비스는 PlayReady 라이선스를 구성할 수 있는 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="88771-107">Media Services also provides APIs that let you configure your PlayReady licenses.</span></span> <span data-ttu-id="88771-108">라이선스에 hello 권한 제한 되도록 hello에 대 한 PlayReady DRM 런타임에서 tooenforce tooplayback 하는 동안 사용자 콘텐츠를 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="88771-108">Licenses contain hello rights and restrictions that you want for hello PlayReady DRM runtime tooenforce when a user is trying tooplayback protected content.</span></span>
<span data-ttu-id="88771-109">지정할 수 있는 PlayReady 라이선스 제한 사항의 몇 가지 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="88771-109">Below are some examples of PlayReady license restrictions that you can specify:</span></span>

* <span data-ttu-id="88771-110">hello는 hello에서 라이선스 유효 날짜/시간입니다.</span><span class="sxs-lookup"><span data-stu-id="88771-110">hello DateTime from which hello license is valid.</span></span>
* <span data-ttu-id="88771-111">hello hello 라이선스 만료 날짜/시간 값입니다.</span><span class="sxs-lookup"><span data-stu-id="88771-111">hello DateTime value when hello license expires.</span></span> 
* <span data-ttu-id="88771-112">에 대 한 hello 라이선스 toobe hello 클라이언트에 영구 저장소에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="88771-112">For hello license toobe saved in persistent storage on hello client.</span></span> <span data-ttu-id="88771-113">영구 라이선스는 일반적으로 사용 되는 tooallow hello 콘텐츠의 오프 라인 재생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88771-113">Persistent licenses are typically used tooallow offline playback of hello content.</span></span>
* <span data-ttu-id="88771-114">hello 최소 보안 수준에는 플레이어는 있어야 tooplay 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="88771-114">hello minimum security level that a player must have tooplay your content.</span></span> 
* <span data-ttu-id="88771-115">hello 출력 오디오 \ 비디오 콘텐츠의 출력 제어 hello에 대 한 보호 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="88771-115">hello output protection level for hello output controls for audio\video content.</span></span> 
* <span data-ttu-id="88771-116">자세한 내용은 참조 hello 출력 제어 섹션 (3.5)에 hello [PlayReady 준수 규칙](https://www.microsoft.com/playready/licensing/compliance/) 문서.</span><span class="sxs-lookup"><span data-stu-id="88771-116">For more information, see hello Output Controls section (3.5) in hello [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>

> [!NOTE]
> <span data-ttu-id="88771-117">현재 hello (이 권한에 필수) hello PlayReady 라이선스의 PlayRight만 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88771-117">Currently, you can only configure hello PlayRight of hello PlayReady license (this right is required).</span></span> <span data-ttu-id="88771-118">hello PlayRight hello 클라이언트 hello 기능 tooplayback hello 콘텐츠를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="88771-118">hello PlayRight gives hello client hello ability tooplayback hello content.</span></span> <span data-ttu-id="88771-119">hello PlayRight에도 제한 특정 tooplayback를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88771-119">hello PlayRight also allows configuring restrictions specific tooplayback.</span></span> <span data-ttu-id="88771-120">자세한 내용은 [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="88771-120">For more information, see [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span></span>
> 
> 

<span data-ttu-id="88771-121">미디어 서비스를 사용 하 여 tooconfigure PlayReady 라이선스를 hello 미디어 서비스 PlayReady 라이선스 템플릿을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="88771-121">tooconfigure PlayReady licenses using Media Services, you must configure hello Media Services PlayReady license template.</span></span> <span data-ttu-id="88771-122">hello 서식 파일은 XML에 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88771-122">hello template is defined in XML.</span></span>

<span data-ttu-id="88771-123">hello 다음 예제에서는 기본 스트리밍 라이선스를 구성 하는 hello 가장 간단한 (및 가장 일반적인) 템플릿</span><span class="sxs-lookup"><span data-stu-id="88771-123">hello following example shows hello simplest (and most common) template that configures a basic streaming license.</span></span> <span data-ttu-id="88771-124">이 라이선스 클라이언트 수 tooplayback 사용할 때 PlayReady 보호 된 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="88771-124">With this license, your clients would be able tooplayback your PlayReady protected content.</span></span>

    <?xml version="1.0" encoding="utf-8"?>
    <PlayReadyLicenseResponseTemplate xmlns:i="http://www.w3.org/2001/XMLSchema-instance" 
                                      xmlns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1">
      <LicenseTemplates>
        <PlayReadyLicenseTemplate>
          <ContentKey i:type="ContentEncryptionKeyFromHeader" />
          <PlayRight />
        </PlayReadyLicenseTemplate>
      </LicenseTemplates>
    </PlayReadyLicenseResponseTemplate>

<span data-ttu-id="88771-125">hello XML hello PlayReady 라이선스 템플릿 XML 스키마 섹션에에서 정의 된 toohello PlayReady 라이선스 템플릿 XML 스키마를 준수 합니다.</span><span class="sxs-lookup"><span data-stu-id="88771-125">hello XML conforms toohello PlayReady license template XML schema defined in hello PlayReady license template XML schema section.</span></span>

<span data-ttu-id="88771-126">또한 미디어 서비스 사용된 tooserialized 및 hello XML에서에서 역직렬화 된 tooand 될 수 있는.NET 클래스 집합을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="88771-126">Media Services also defines a set of .NET classes that could be used tooserialized and deserialized tooand from hello XML.</span></span> <span data-ttu-id="88771-127">기본 클래스에 대한 설명은 [Media Services .NET 클래스](media-services-playready-license-template-overview.md#classes)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="88771-127">For description of main classes, see [Media Services .NET classes](media-services-playready-license-template-overview.md#classes).</span></span> <span data-ttu-id="88771-128">되 tooconfigure 사용 되는 라이선스 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="88771-128">that are used tooconfigure license templates.</span></span>

<span data-ttu-id="88771-129">.NET을 사용 하는 종단 간 예제 tooconfigure hello PlayReady 라이선스 템플릿을 클래스에 대 한 참조 [를 사용 하 여 PlayReady 동적 암호화 및 라이선스 배달 서비스](media-services-protect-with-drm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="88771-129">For an end-to-end example that uses .NET classes tooconfigure hello PlayReady license template, see [Using PlayReady Dynamic Encryption and License Delivery Service](media-services-protect-with-drm.md).</span></span>

## <span data-ttu-id="88771-130"><a id="classes"></a>미디어 서비스.NET 클래스에 사용 되는 tooconfigure 라이선스 템플릿</span><span class="sxs-lookup"><span data-stu-id="88771-130"><a id="classes"></a>Media Services .NET classes that are used tooconfigure license templates</span></span>
<span data-ttu-id="88771-131">hello 주.NET 클래스는 사용 되는 tooconfigure 미디어 서비스 PlayReady 라이선스 템플릿은 hello 다음과가 같습니다.</span><span class="sxs-lookup"><span data-stu-id="88771-131">hello following are hello main .NET classes are used tooconfigure Media Services PlayReady license templates.</span></span> <span data-ttu-id="88771-132">이러한 클래스에 정의 된 toohello 형식을 매핑할 [PlayReady 라이선스 템플릿 XML 스키마](media-services-playready-license-template-overview.md#schema)합니다.</span><span class="sxs-lookup"><span data-stu-id="88771-132">These classes map toohello types defined in [PlayReady license template XML schema](media-services-playready-license-template-overview.md#schema).</span></span>

<span data-ttu-id="88771-133">hello [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) 클래스가 사용 되는 tooserialize 고 tooand hello 미디어 서비스 라이선스 템플릿 XML에서에서 역직렬화 합니다.</span><span class="sxs-lookup"><span data-stu-id="88771-133">hello [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) class is used tooserialize and deserialize tooand from hello Media Services license template XML.</span></span>

### <a name="playreadylicenseresponsetemplate"></a><span data-ttu-id="88771-134">PlayReadyLicenseResponseTemplate</span><span class="sxs-lookup"><span data-stu-id="88771-134">PlayReadyLicenseResponseTemplate</span></span>
<span data-ttu-id="88771-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) -hello 응답 전송 백 toohello 최종 사용자에 대 한이 클래스는 hello 서식 파일을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="88771-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) - This class represents hello template for hello response sent back toohello end user.</span></span> <span data-ttu-id="88771-136">하나 이상의 라이선스 템플릿 목록 뿐 아니라 hello 라이선스 서버 hello 응용 프로그램 (사용자 지정 앱 논리에 유용할 수 있습니다) 사이는 사용자 지정 데이터 문자열에 대 한 필드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="88771-136">It contains a field for a custom data string between hello license server and hello application (may be useful for custom app logic) as well as a list of one or more license templates.</span></span>

<span data-ttu-id="88771-137">Hello 템플릿 계층 구조에서 hello "최상위" 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="88771-137">This is hello “top level” class in hello template hierarchy.</span></span> <span data-ttu-id="88771-138">Hello 응답 템플릿에 라이선스 템플릿 목록이 포함 되어 있으며 (직접 또는 간접적으로) hello 라이선스 템플릿에 포함 되어 있음을 의미 hello 템플릿 데이터 toobe 직렬화를 구성 하는 다른 클래스의 모든 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="88771-138">Meaning that hello response template includes a list of license templates and hello license templates include (directly or indirectly) all of hello other classes that make up hello template data toobe serialized.</span></span>

### <a name="playreadylicensetemplate"></a><span data-ttu-id="88771-139">PlayReadyLicenseTemplate</span><span class="sxs-lookup"><span data-stu-id="88771-139">PlayReadyLicenseTemplate</span></span>
<span data-ttu-id="88771-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) -hello 클래스 toohello 최종 사용자가 반환 하는 PlayReady 라이선스 toobe를 만들기 위한 라이선스 템플릿을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="88771-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) - hello class represents a license template for creating PlayReady licenses toobe returned toohello end users.</span></span> <span data-ttu-id="88771-141">Hello hello 라이선스에 hello 콘텐츠 키에는 데이터를 포함 하며 모든 권한 또는 제한 toobe에 의해 적용 hello PlayReady DRM 런타임에서 hello 콘텐츠 키를 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="88771-141">It contains hello data on hello content key in hello license and any rights or restrictions toobe enforced by hello PlayReady DRM runtime when using hello content key.</span></span>

### <span data-ttu-id="88771-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span><span class="sxs-lookup"><span data-stu-id="88771-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span></span>
<span data-ttu-id="88771-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) -이 클래스는 hello PlayReady 라이선스의 PlayRight를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="88771-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) - This class represents hello PlayRight of a PlayReady license.</span></span> <span data-ttu-id="88771-144">콘텐츠 제목 toohello 0 hello 또는 hello 라이선스 및 PlayRight 자체 (재생 관련 정책의 경우) hello에 대 한 제한 구성 hello 사용자 hello 기능 tooplayback를 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="88771-144">It grants hello user hello ability tooplayback hello content subject toohello zero or more restrictions configured in hello license and on hello PlayRight itself (for playback specific policy).</span></span> <span data-ttu-id="88771-145">Toodo hello hello 콘텐츠를 재생할 수 있는 출력 종류를 제어 하는 출력 제한 사항 및 제한 되어야 하는 위치에 지정된 된 출력을 사용 하는 경우에 hello 정책 hello PlayRight에 많이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88771-145">Much of hello policy on hello PlayRight has toodo with output restrictions which control hello types of outputs that hello content can be played over and any restrictions that must be put in place when using a given output.</span></span> <span data-ttu-id="88771-146">예를 들어 DigitalVideoOnlyContentRestriction을 사용 하는 hello 다음 hello 경우 DRM 런타임은 하면 hello 비디오 toobe (아날로그 비디오 출력 사용 하지 못하는 toopass hello 콘텐츠) 디지털 출력을 통해 표시.</span><span class="sxs-lookup"><span data-stu-id="88771-146">For example, if hello DigitalVideoOnlyContentRestriction is enabled, then hello DRM runtime will only allow hello video toobe displayed over digital outputs (analog video outputs won’t be allowed toopass hello content).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="88771-147">이러한 종류의 제한 사항은 매우 강력 할 수 있지만 hello 소비자 환경에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88771-147">These types of restrictions can be very powerful but can also affect hello consumer experience.</span></span> <span data-ttu-id="88771-148">Hello 출력 보호가 너무 제한적으로 구성 된 hello 콘텐츠가 일부 클라이언트에서 재생 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88771-148">If hello output protections are configured too restrictive, hello content might be unplayable on some clients.</span></span> <span data-ttu-id="88771-149">자세한 내용은 참조 hello [PlayReady 준수 규칙](https://www.microsoft.com/playready/licensing/compliance/) 문서.</span><span class="sxs-lookup"><span data-stu-id="88771-149">For more information, see hello [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>
> 
> 

<span data-ttu-id="88771-150">Silverlight에서 지원하는 보호 수준의 예는 [출력 보호를 위한 Silverlight 지원](http://go.microsoft.com/fwlink/?LinkId=617318)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="88771-150">For an example of what protection levels Silverlight supports, see: [Silverlight support for output protections](http://go.microsoft.com/fwlink/?LinkId=617318).</span></span>

## <span data-ttu-id="88771-151"><a id="schema"></a>PlayReady 라이선스 템플릿 XML 스키마</span><span class="sxs-lookup"><span data-stu-id="88771-151"><a id="schema"></a>PlayReady license template XML schema</span></span>
    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:tns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1" xmlns:ser="http://schemas.microsoft.com/2003/10/Serialization/" elementFormDefault="qualified" targetNamespace="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1" xmlns:xs="http://www.w3.org/2001/XMLSchema">
      <xs:import namespace="http://schemas.microsoft.com/2003/10/Serialization/" />
      <xs:complexType name="AgcAndColorStripeRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="AgcAndColorStripeRestriction" nillable="true" type="tns:AgcAndColorStripeRestriction" />
      <xs:simpleType name="ContentType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Unspecified" />
          <xs:enumeration value="UltravioletDownload" />
          <xs:enumeration value="UltravioletStreaming" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="ContentType" nillable="true" type="tns:ContentType" />
      <xs:complexType name="ExplicitAnalogTelevisionRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="BestEffort" type="xs:boolean" />
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ExplicitAnalogTelevisionRestriction" nillable="true" type="tns:ExplicitAnalogTelevisionRestriction" />
      <xs:complexType name="PlayReadyContentKey">
        <xs:sequence />
      </xs:complexType>
      <xs:element name="PlayReadyContentKey" nillable="true" type="tns:PlayReadyContentKey" />
      <xs:complexType name="ContentEncryptionKeyFromHeader">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:PlayReadyContentKey">
            <xs:sequence />
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="ContentEncryptionKeyFromHeader" nillable="true" type="tns:ContentEncryptionKeyFromHeader" />
      <xs:complexType name="ContentEncryptionKeyFromKeyIdentifier">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:PlayReadyContentKey">
            <xs:sequence>
              <xs:element minOccurs="0" name="KeyIdentifier" type="ser:guid" />
            </xs:sequence>
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="ContentEncryptionKeyFromKeyIdentifier" nillable="true" type="tns:ContentEncryptionKeyFromKeyIdentifier" />
      <xs:complexType name="PlayReadyLicenseResponseTemplate">
        <xs:sequence>
          <xs:element name="LicenseTemplates" nillable="true" type="tns:ArrayOfPlayReadyLicenseTemplate" />
          <xs:element minOccurs="0" name="ResponseCustomData" nillable="true" type="xs:string">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyLicenseResponseTemplate" nillable="true" type="tns:PlayReadyLicenseResponseTemplate" />
      <xs:complexType name="ArrayOfPlayReadyLicenseTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="PlayReadyLicenseTemplate" nillable="true" type="tns:PlayReadyLicenseTemplate" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfPlayReadyLicenseTemplate" nillable="true" type="tns:ArrayOfPlayReadyLicenseTemplate" />
      <xs:complexType name="PlayReadyLicenseTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" name="AllowTestDevices" type="xs:boolean" />
          <xs:element minOccurs="0" name="BeginDate" nillable="true" type="xs:dateTime">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element name="ContentKey" nillable="true" type="tns:PlayReadyContentKey" />
          <xs:element minOccurs="0" name="ContentType" type="tns:ContentType">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ExpirationDate" nillable="true" type="xs:dateTime">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="GracePeriod" nillable="true" type="ser:duration">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="LicenseType" type="tns:PlayReadyLicenseType" />
          <xs:element minOccurs="0" name="PlayRight" nillable="true" type="tns:PlayReadyPlayRight" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyLicenseTemplate" nillable="true" type="tns:PlayReadyLicenseTemplate" />
      <xs:simpleType name="PlayReadyLicenseType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Nonpersistent" />
          <xs:enumeration value="Persistent" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="PlayReadyLicenseType" nillable="true" type="tns:PlayReadyLicenseType" />
      <xs:complexType name="PlayReadyPlayRight">
        <xs:sequence>
          <xs:element minOccurs="0" name="AgcAndColorStripeRestriction" nillable="true" type="tns:AgcAndColorStripeRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="AllowPassingVideoContentToUnknownOutput" type="tns:UnknownOutputPassingOption">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="AnalogVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="CompressedDigitalAudioOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="CompressedDigitalVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="DigitalVideoOnlyContentRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ExplicitAnalogTelevisionOutputRestriction" nillable="true" type="tns:ExplicitAnalogTelevisionRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="FirstPlayExpiration" nillable="true" type="ser:duration">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ImageConstraintForAnalogComponentVideoRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ImageConstraintForAnalogComputerMonitorRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ScmsRestriction" nillable="true" type="tns:ScmsRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="UncompressedDigitalAudioOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="UncompressedDigitalVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyPlayRight" nillable="true" type="tns:PlayReadyPlayRight" />
      <xs:simpleType name="UnknownOutputPassingOption">
        <xs:restriction base="xs:string">
          <xs:enumeration value="NotAllowed" />
          <xs:enumeration value="Allowed" />
          <xs:enumeration value="AllowedWithVideoConstriction" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="UnknownOutputPassingOption" nillable="true" type="tns:UnknownOutputPassingOption" />
      <xs:complexType name="ScmsRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ScmsRestriction" nillable="true" type="tns:ScmsRestriction" />
    </xs:schema>



## <a name="media-services-learning-paths"></a><span data-ttu-id="88771-152">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="88771-152">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="88771-153">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="88771-153">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

