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
# <a name="media-services-playready-license-template-overview"></a>Media Services PlayReady 라이선스 템플릿 개요
Azure 미디어 서비스는 현재 Microsoft PlayReady 라이선스를 배달하는 서비스를 제공합니다. Hello 최종 사용자 플레이어 (예: Silverlight) tooplay 하려고 할 때 PlayReady 보호 된 콘텐츠, 보낸된 toohello 라이선스 배달 서비스 tooobtain 라이선스를 요청 합니다. Hello 라이선스 서비스 hello 요청을 승인 하는 경우 보낸된 toohello 클라이언트 중인 hello 라이선스를 발급 하 고 수 수 사용된 toodecrypt 앤 플레이 hello 지정 된 콘텐츠입니다.

또한 미디어 서비스는 PlayReady 라이선스를 구성할 수 있는 API를 제공합니다. 라이선스에 hello 권한 제한 되도록 hello에 대 한 PlayReady DRM 런타임에서 tooenforce tooplayback 하는 동안 사용자 콘텐츠를 보호 합니다.
지정할 수 있는 PlayReady 라이선스 제한 사항의 몇 가지 예는 다음과 같습니다.

* hello는 hello에서 라이선스 유효 날짜/시간입니다.
* hello hello 라이선스 만료 날짜/시간 값입니다. 
* 에 대 한 hello 라이선스 toobe hello 클라이언트에 영구 저장소에 저장 합니다. 영구 라이선스는 일반적으로 사용 되는 tooallow hello 콘텐츠의 오프 라인 재생 됩니다.
* hello 최소 보안 수준에는 플레이어는 있어야 tooplay 콘텐츠입니다. 
* hello 출력 오디오 \ 비디오 콘텐츠의 출력 제어 hello에 대 한 보호 수준입니다. 
* 자세한 내용은 참조 hello 출력 제어 섹션 (3.5)에 hello [PlayReady 준수 규칙](https://www.microsoft.com/playready/licensing/compliance/) 문서.

> [!NOTE]
> 현재 hello (이 권한에 필수) hello PlayReady 라이선스의 PlayRight만 구성할 수 있습니다. hello PlayRight hello 클라이언트 hello 기능 tooplayback hello 콘텐츠를 제공합니다. hello PlayRight에도 제한 특정 tooplayback를 구성할 수 있습니다. 자세한 내용은 [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight)를 참조하세요.
> 
> 

미디어 서비스를 사용 하 여 tooconfigure PlayReady 라이선스를 hello 미디어 서비스 PlayReady 라이선스 템플릿을 구성 해야 합니다. hello 서식 파일은 XML에 정의 됩니다.

hello 다음 예제에서는 기본 스트리밍 라이선스를 구성 하는 hello 가장 간단한 (및 가장 일반적인) 템플릿 이 라이선스 클라이언트 수 tooplayback 사용할 때 PlayReady 보호 된 콘텐츠입니다.

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

hello XML hello PlayReady 라이선스 템플릿 XML 스키마 섹션에에서 정의 된 toohello PlayReady 라이선스 템플릿 XML 스키마를 준수 합니다.

또한 미디어 서비스 사용된 tooserialized 및 hello XML에서에서 역직렬화 된 tooand 될 수 있는.NET 클래스 집합을 정의 합니다. 기본 클래스에 대한 설명은 [Media Services .NET 클래스](media-services-playready-license-template-overview.md#classes)를 참조하세요. 되 tooconfigure 사용 되는 라이선스 템플릿입니다.

.NET을 사용 하는 종단 간 예제 tooconfigure hello PlayReady 라이선스 템플릿을 클래스에 대 한 참조 [를 사용 하 여 PlayReady 동적 암호화 및 라이선스 배달 서비스](media-services-protect-with-drm.md)합니다.

## <a id="classes"></a>미디어 서비스.NET 클래스에 사용 되는 tooconfigure 라이선스 템플릿
hello 주.NET 클래스는 사용 되는 tooconfigure 미디어 서비스 PlayReady 라이선스 템플릿은 hello 다음과가 같습니다. 이러한 클래스에 정의 된 toohello 형식을 매핑할 [PlayReady 라이선스 템플릿 XML 스키마](media-services-playready-license-template-overview.md#schema)합니다.

hello [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) 클래스가 사용 되는 tooserialize 고 tooand hello 미디어 서비스 라이선스 템플릿 XML에서에서 역직렬화 합니다.

### <a name="playreadylicenseresponsetemplate"></a>PlayReadyLicenseResponseTemplate
[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) -hello 응답 전송 백 toohello 최종 사용자에 대 한이 클래스는 hello 서식 파일을 나타냅니다. 하나 이상의 라이선스 템플릿 목록 뿐 아니라 hello 라이선스 서버 hello 응용 프로그램 (사용자 지정 앱 논리에 유용할 수 있습니다) 사이는 사용자 지정 데이터 문자열에 대 한 필드를 포함 합니다.

Hello 템플릿 계층 구조에서 hello "최상위" 클래스입니다. Hello 응답 템플릿에 라이선스 템플릿 목록이 포함 되어 있으며 (직접 또는 간접적으로) hello 라이선스 템플릿에 포함 되어 있음을 의미 hello 템플릿 데이터 toobe 직렬화를 구성 하는 다른 클래스의 모든 hello 합니다.

### <a name="playreadylicensetemplate"></a>PlayReadyLicenseTemplate
[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) -hello 클래스 toohello 최종 사용자가 반환 하는 PlayReady 라이선스 toobe를 만들기 위한 라이선스 템플릿을 나타냅니다. Hello hello 라이선스에 hello 콘텐츠 키에는 데이터를 포함 하며 모든 권한 또는 제한 toobe에 의해 적용 hello PlayReady DRM 런타임에서 hello 콘텐츠 키를 사용 하는 경우.

### <a id="PlayReadyPlayRight"></a>PlayReadyPlayRight
[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) -이 클래스는 hello PlayReady 라이선스의 PlayRight를 나타냅니다. 콘텐츠 제목 toohello 0 hello 또는 hello 라이선스 및 PlayRight 자체 (재생 관련 정책의 경우) hello에 대 한 제한 구성 hello 사용자 hello 기능 tooplayback를 부여 합니다. Toodo hello hello 콘텐츠를 재생할 수 있는 출력 종류를 제어 하는 출력 제한 사항 및 제한 되어야 하는 위치에 지정된 된 출력을 사용 하는 경우에 hello 정책 hello PlayRight에 많이 있습니다. 예를 들어 DigitalVideoOnlyContentRestriction을 사용 하는 hello 다음 hello 경우 DRM 런타임은 하면 hello 비디오 toobe (아날로그 비디오 출력 사용 하지 못하는 toopass hello 콘텐츠) 디지털 출력을 통해 표시.

> [!IMPORTANT]
> 이러한 종류의 제한 사항은 매우 강력 할 수 있지만 hello 소비자 환경에 영향을 줄 수 있습니다. Hello 출력 보호가 너무 제한적으로 구성 된 hello 콘텐츠가 일부 클라이언트에서 재생 수 있습니다. 자세한 내용은 참조 hello [PlayReady 준수 규칙](https://www.microsoft.com/playready/licensing/compliance/) 문서.
> 
> 

Silverlight에서 지원하는 보호 수준의 예는 [출력 보호를 위한 Silverlight 지원](http://go.microsoft.com/fwlink/?LinkId=617318)을 참조하세요.

## <a id="schema"></a>PlayReady 라이선스 템플릿 XML 스키마
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



## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

