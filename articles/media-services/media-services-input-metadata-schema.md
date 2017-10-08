---
title: "미디어 서비스 입력된 메타 데이터 스키마 aaaAzure | Microsoft Docs"
description: "hello 항목에서는 Azure 미디어 서비스 입력된 메타 데이터 스키마에 대 한 개요를 제공 합니다."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: d72848e2-4b65-4c84-94bc-e2a90a6e7f47
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 9b72c6ff317aa98451ea75548465dc6023b44a55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="input-metadata"></a>입력 메타데이터
인코딩 작업은 입력된 자산 (또는 자산)와 연결 하려는 tooperform 몇 가지 인코딩 작업 합니다.  태스크가 완료되는 즉시 출력 자산이 생성됩니다.  hello 출력 자산은 비디오, 오디오, 미리 보기, 매니페스트 포함, 등 hello 출력 자산도 hello 입력된 자산 관련 메타 데이터가 있는 파일을 포함 합니다. hello hello 메타 데이터 XML 파일의 이름에 형식에 따라 hello: &lt;t _ i d&gt;_ m e (예를 들어 41114ad3 eb5e-4 c-57-8 d 92-5354e2b7d4a4_metadata.xml), 여기서 &lt;t _ i d&gt; 는 hello AssetId hello 입력 자산의 값입니다.  

Tooexamine hello 메타 데이터 파일을 원하는 경우 만들 수 있습니다는 **SAS** 로케이터 및 다운로드 hello 파일 tooyour 로컬 컴퓨터입니다. 방법에 대 한 예제를 찾을 수 toocreate SAS 로케이터 파일을 다운로드 하 고 [hello 미디어 서비스.NET SDK Extensions를 사용 하 여](media-services-dotnet-get-started.md)합니다.  

이 항목에서는 어떤 hello 입력된 메타 데이터가에 hello 요소 및 형식의 hello XML 스키마를 설명 (&lt;t _ i d&gt;_ m e) 기반 합니다.  Hello 출력 자산 관련 메타 데이터가 포함 된 hello 파일에 대 한 정보를 참조 하십시오. [출력 메타 데이터](media-services-output-metadata-schema.md)합니다.  

> [!NOTE]
> Hello를 찾을 수 있습니다 [스키마 코드](media-services-input-metadata-schema.md#code) 는 [XML 예제](media-services-input-metadata-schema.md#xml) 이 항목의 hello 끝에 있습니다.  
> 
> 

## <a name="AssetFiles"></a> AssetFiles 요소(루트 요소)
컬렉션을 포함 [AssetFile 요소](media-services-input-metadata-schema.md#AssetFile)hello 인코딩 작업에 대 한 합니다.  

이 항목의 hello 끝에 XML 예제: [XML 예제](media-services-input-metadata-schema.md#xml)합니다.  

| 이름 | 설명 |
| --- | --- |
| **AssetFile**<br /><br /> minOccurs="1" maxOccurs="unbounded" |단일 자식 요소입니다. 자세한 내용은 [AssetFile 요소](media-services-input-metadata-schema.md#AssetFile)를 참조하세요. |

## <a name="AssetFile"></a> AssetFile 요소
 자산 파일을 설명하는 속성과 요소를 포함하고 있습니다.  

 이 항목의 hello 끝에 XML 예제: [XML 예제](media-services-input-metadata-schema.md#xml)합니다.  

### <a name="attributes"></a>특성
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **Name**<br /><br /> 필수 |**xs:string** |자산 파일의 이름입니다. |
| **크기**<br /><br /> 필수 |**xs:long** |바이트 단위로 hello 자산 파일의 크기입니다. |
| **Duration**<br /><br /> 필수 |**xs:duration** |콘텐츠 재생 시간입니다. 예제: Duration="PT25M37.757S" |
| **NumberOfStreams**<br /><br /> 필수 |**xs:int** |Hello 자산 파일의 스트림 수입니다. |
| **FormatNames**<br /><br /> 필수 |**xs:string** |형식 이름입니다. |
| **FormatVerboseNames**<br /><br /> 필수 |**xs:string** |자세한 형식 이름입니다. |
| **StartTime** |**xs:duration** |콘텐츠 시작 시간입니다. 예제: StartTime="PT2.669S" |
| **OverallBitRate** |**xs:int** |Kbps에서 hello 자산 파일의 평균 비트입니다. |

> [!NOTE]
> 다음과 같은 4 자식 요소가 hello 시퀀스에 나타나야 합니다.  
> 
> 

### <a name="child-elements"></a>자식 요소
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **Programs**<br /><br /> minOccurs="0" | |모든 컬렉션 [프로그램 요소](media-services-input-metadata-schema.md#Programs) 때 hello 자산 파일이 MPEG-TS 형태로 표시 합니다. |
| **VideoTracks**<br /><br /> minOccurs="0" | |각각의 실제 자산 파일에는 적절한 컨테이너 형식으로 인터리빙된 0개 이상의 비디오 트랙이 포함될 수 있습니다. 이 요소는 모든 컬렉션을 포함 [VideoTracks 요소](media-services-input-metadata-schema.md#VideoTracks) hello 자산 파일의 일부인 합니다. |
| **AudioTracks**<br /><br /> minOccurs="0" | |각각의 실제 자산 파일에는 적절한 컨테이너 형식으로 인터리빙된 0개 이상의 오디오 트랙이 포함될 수 있습니다. 이 요소는 모든 컬렉션을 포함 [AudioTracks 요소](media-services-input-metadata-schema.md#AudioTracks) hello 자산 파일의 일부인 합니다. |
| **Metadata**<br /><br /> minOccurs="0" maxOccurs="unbounded" |[MetadataType](media-services-input-metadata-schema.md#MetadataType) |key/value 문자열로 표시되는 자산 파일의 메타데이터입니다. 예:<br /><br /> **&lt;Metadata key="language" value="eng" /&gt;** |

## <a name="TrackType"></a> TrackType
이 항목의 hello 끝에 XML 예제: [XML 예제](media-services-input-metadata-schema.md#xml)합니다.  

### <a name="attributes"></a>특성
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **Id**<br /><br /> 필수 |**xs:int** |이 오디오 또는 비디오 트랙의 0 기준 인덱스입니다.<br /><br /> 이 아닌 경우 반드시 해당 hello MP4 파일에서 사용 되는 TrackID |
| **Codec** |**xs:string** |비디오 트랙 코덱 문자열입니다. |
| **CodecLongName** |**xs:string** |오디오 또는 비디오 트랙 코덱의 긴 이름입니다. |
| **TimeBase**<br /><br /> 필수 |**xs:string** |시간 기준입니다. 예제: TimeBase="1/48000" |
| **NumberOfFrames** |**xs:int** |프레임 수입니다(비디오 트랙의 경우). |
| **StartTime** |**xs:duration** |트랙 시작 시간입니다. 예제: StartTime="PT2.669S" |
| **Duration** |**xs:duration** |트랙 지속 시간입니다. 예제: Duration="PTSampleFormat M37.757S" |

> [!NOTE]
> 다음과 같은 2 자식 요소가 hello 시퀀스에 나타나야 합니다.  
> 
> 

### <a name="child-elements"></a>자식 요소
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **Disposition**<br /><br /> minOccurs="0" maxOccurs="1" |[StreamDispositionType](media-services-input-metadata-schema.md#StreamDispositionType) |프레젠테이션 정보가 포함됩니다(예: 특정 오디오 트랙이 시각 장애 시청자를 위한 것인지 여부). |
| **Metadata**<br /><br /> minOccurs="0" maxOccurs="unbounded" |[MetadataType](media-services-input-metadata-schema.md#MetadataType) |사용 되는 toohold 다양 한 일 수 있는 일반 키/값 문자열입니다. 예제: key=”language” 및 value=”eng” |

## <a name="AudioTrackType"></a> AudioTrackType(TrackType에서 상속)
 **AudioTrackType**는 [TrackType](media-services-input-metadata-schema.md#TrackType)에서 상속되는 전역 복합 형식입니다.  

 hello 형식은 hello 자산 파일의 특정 오디오 트랙을 나타냅니다.  

 이 항목의 hello 끝에 XML 예제: [XML 예제](media-services-input-metadata-schema.md#xml)합니다.  

### <a name="attributes"></a>특성
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **SampleFormat** |**xs:string** |샘플 형식입니다. |
| **ChannelLayout** |**xs:string** |채널 레이아웃입니다. |
| **Channels**<br /><br /> 필수 |**xs:int** |오디오 채널 수입니다(0개 이상). |
| **SamplingRate**<br /><br /> 필수 |**xs:int** |오디오 샘플링 속도(샘플/초 또는 Hz)입니다. |
| **Bitrate** |**xs:int** |Hello 자산 파일에서 계산 되는 초당 비트 단위의 평균 오디오 비트 속도입니다. Hello 기본 스트림 페이로드만 계산 되며 및 hello 패키징 오버 헤드는이 개수에 포함 되지 않습니다. |
| **BitsPerSample** |**xs:int** |Hello wFormatTag 형식에 대 한 샘플당 비트를 입력합니다. |

## <a name="VideoTrackType"></a> VideoTrackType(TrackType에서 상속)
**VideoTrackType**는 [TrackType](media-services-input-metadata-schema.md#TrackType)에서 상속되는 전역 복합 형식입니다.  

hello 형식은 hello 자산 파일의 특정 비디오 트랙을 나타냅니다.  

이 항목의 hello 끝에 XML 예제: [XML 예제](media-services-input-metadata-schema.md#xml)합니다.  

### <a name="attributes"></a>특성
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **FourCC**<br /><br /> 필수 |**xs:string** |비디오 코덱 FourCC 코드입니다. |
| **프로필** |**xs:string** |비디오 트랙의 프로필입니다. |
| **Level** |**xs:string** |비디오 트랙의 수준입니다. |
| **PixelFormat** |**xs:string** |비디오 트랙의 픽셀 형식입니다. |
| **Width**<br /><br /> 필수 |**xs:int** |인코딩된 비디오 너비(픽셀)입니다. |
| **Height**<br /><br /> 필수 |**xs:int** |인코딩된 비디오 높이(픽셀)입니다. |
| **DisplayAspectRatioNumerator**<br /><br /> 필수 |**xs:double** |비디오 디스플레이 가로 세로 비율의 분자입니다. |
| **DisplayAspectRatioDenominator**<br /><br /> 필수 |**xs:double** |비디오 디스플레이 가로 세로 비율의 분모입니다. |
| **DisplayAspectRatioDenominator**<br /><br /> 필수 |**xs:double** |비디오 샘플 가로 세로 비율의 분자입니다. |
| **SampleAspectRatioNumerator** |**xs:double** |비디오 샘플 가로 세로 비율의 분자입니다. |
| **SampleAspectRatioNumerator** |**xs:double** |비디오 샘플 가로 세로 비율의 분모입니다. |
| **FrameRate**<br /><br /> 필수 |**xs: decimal** |.3f 형식으로 측정된 비디오 프레임 속도입니다. |
| **Bitrate** |**xs:int** |Hello 자산 파일에서 계산 된 대로 k b / 초, 평균 비디오 비트 속도입니다. Hello 기본 스트림 페이로드만 계산 되며 및 hello 패키징 오버 헤드는 포함 되지 않습니다. |
| **MaxGOPBitrate** |**xs:int** |이 비디오 트랙의 최대 GOP 평균 비트 전송률(Kb/초)입니다. |
| **HasBFrames** |**xs:int** |B 프레임의 비디오 트랙 번호입니다. |

## <a name="MetadataType"></a> MetadataType
**MetadataType**은 자산 파일의 메타데이터를 key/value 문자열로 설명하는 전역 복합 형식입니다. 예제: key=”language” 및 value=”eng”  

이 항목의 hello 끝에 XML 예제: [XML 예제](media-services-input-metadata-schema.md#xml)합니다.  

### <a name="attributes"></a>특성
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **key**<br /><br /> 필수 |**xs:string** |hello 키/값 쌍의 hello 키입니다. |
| **값**<br /><br /> 필수 |**xs:string** |hello 키/값 쌍의 hello 값입니다. |

## <a name="ProgramType"></a> ProgramType
**ProgramType**은 프로그램을 설명하는 전역 복합 형식입니다.  

### <a name="attributes"></a>특성
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **ProgramId**<br /><br /> 필수 |**xs:int** |Program ID입니다. |
| **NumberOfPrograms**<br /><br /> 필수 |**xs:int** |프로그램 수입니다. |
| **PmtPid**<br /><br /> 필수 |**xs:int** |PMT(프로그램 맵 테이블)에는 프로그램에 대한 정보가 포함됩니다.  자세한 내용은 [PMT](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT)를 참조하세요. |
| **PcrPid**<br /><br /> 필수 |**xs:int** |디코더에서 사용됩니다. 자세한 내용은 [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR)을 참조하세요. |
| **StartPTS** |**xs: long** |프레젠테이션 시작 타임스탬프입니다. |
| **EndPTS** |**xs: long** |프레젠테이션 끝 타임스탬프입니다. |

## <a name="StreamDispositionType"></a> StreamDispositionType
**StreamDispositionType** 는 hello 스트림을 설명 하는 전역 복합 유형입니다.  

이 항목의 hello 끝에 XML 예제: [XML 예제](media-services-input-metadata-schema.md#xml)합니다.  

### <a name="attributes"></a>특성
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **기본값**<br /><br /> 필수 |**xs:int** |이이 특성 too1 tooindicate hello 기본 표시가 설정 합니다. |
| **Dub**<br /><br /> 필수 |**xs:int** |설정 합니다.이 특성 too1 tooindicate 프레젠테이션 더빙 hello 합니다. |
| **Original**<br /><br /> 필수 |**xs:int** |이이 특성 too1 tooindicate hello 원본 표시를 설정 합니다. |
| **Comment**<br /><br /> 필수 |**xs:int** |설정 합니다.이 특성 too1 tooindicate 트랙에 설명이 포함 되어 있습니다. |
| **Lyrics**<br /><br /> 필수 |**xs:int** |설정 합니다.이 특성 too1 tooindicate 트랙에 가사가 포함 되어 있습니다. |
| **Karaoke**<br /><br /> 필수 |**xs:int** |설정 합니다.이 특성 too1 tooindicate 나타냅니다 hello이 항목이 가라오케 트랙 (배경 음악, 보컬 없음). |
| **Forced**<br /><br /> 필수 |**xs:int** |이이 특성 too1 tooindicate 강제 hello 프레젠테이션을 설정 합니다. |
| **HearingImpaired**<br /><br /> 필수 |**xs:int** |이 특성 too1 tooindicate hello 항목이 청각 장애 자용 임을 설정 합니다. |
| **VisualImpaired**<br /><br /> 필수 |**xs:int** |이 트랙은 시각 장애가 있는 hello에 대 한이 특성 too1 tooindicate를 설정 합니다. |
| **CleanEffects**<br /><br /> 필수 |**xs:int** |이 트랙에이 특성 too1 tooindicate 클린 효과 설정 합니다. |
| **AttachedPic**<br /><br /> 필수 |**xs:int** |이 트랙에이 특성 too1 tooindicate 그림을 설정 합니다. |

## <a name="Programs"></a> Programs 요소
여러 **Program** 요소를 보유하는 래퍼 요소입니다.  

### <a name="child-elements"></a>자식 요소
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **Program**<br /><br /> minOccurs="0" maxOccurs="unbounded" |[ProgramType](media-services-input-metadata-schema.md#ProgramType) |MPEG-TS 형식인 자산 파일에 대 한 hello 자산 파일의 프로그램에 대 한 정보를 포함 합니다. |

## <a name="VideoTracks"></a> VideoTracks 요소
 여러 **VideoTrack** 요소를 보유하는 래퍼 요소입니다.  

 이 항목의 hello 끝에 XML 예제: [XML 예제](media-services-input-metadata-schema.md#xml)합니다.  

### <a name="child-elements"></a>자식 요소
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **VideoTrack**<br /><br /> minOccurs="0" maxOccurs="unbounded" |[VideoTrackType(TrackType에서 상속)](media-services-input-metadata-schema.md#VideoTrackType) |Hello 자산 파일의 비디오 트랙에 대 한 정보를 포함합니다. |

## <a name="AudioTracks"></a> AudioTracks 요소
 여러 **AudioTrack** 요소를 보유하는 래퍼 요소입니다.  

 이 항목의 hello 끝에 XML 예제: [XML 예제](media-services-input-metadata-schema.md#xml)합니다.  

### <a name="elements"></a>요소
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **AudioTrack**<br /><br /> minOccurs="0" maxOccurs="unbounded" |[AudioTrackType(TrackType에서 상속)](media-services-input-metadata-schema.md#AudioTrackType) |Hello 자산 파일의 오디오 트랙에 대 한 정보를 포함합니다. |

## <a name="code"></a> 스키마 코드
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.0"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               elementFormDefault="qualified">  

      <xs:complexType name="MetadataType">  
        <xs:attribute name="key"   type="xs:string" use="required"/>  
        <xs:attribute name="value" type="xs:string" use="required"/>  
      </xs:complexType>  

      <xs:complexType name="ProgramType">  
        <xs:attribute name="ProgramId" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Program Id</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfPrograms" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Number of programs</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PmtPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pmt pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PcrPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pcr pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="StartPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>start pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="EndPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>end pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="StreamDispositionType">  
        <xs:attribute name="Default"          type="xs:int" use="required" />  
        <xs:attribute name="Dub"              type="xs:int" use="required" />  
        <xs:attribute name="Original"         type="xs:int" use="required" />  
        <xs:attribute name="Comment"          type="xs:int" use="required" />  
        <xs:attribute name="Lyrics"           type="xs:int" use="required" />  
        <xs:attribute name="Karaoke"          type="xs:int" use="required" />  
        <xs:attribute name="Forced"           type="xs:int" use="required" />  
        <xs:attribute name="HearingImpaired"  type="xs:int" use="required" />  
        <xs:attribute name="VisualImpaired"   type="xs:int" use="required" />  
        <xs:attribute name="CleanEffects"     type="xs:int" use="required" />  
        <xs:attribute name="AttachedPic"      type="xs:int" use="required" />  
      </xs:complexType>  

      <xs:complexType name="TrackType" abstract="true">  
        <xs:sequence>  
          <xs:element name="Disposition" type="StreamDispositionType" minOccurs="0" maxOccurs="1"/>  
          <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded"/>  
        </xs:sequence>  
        <xs:attribute name="Id" use="required">  
          <xs:annotation>  
            <xs:documentation>zero-based index of this video track. Note: this is not necessarily hello TrackID as used in an MP4 file</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="Codec" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec string</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="CodecLongName" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec long name</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="TimeBase"  type="xs:string" use="required">  
          <xs:annotation>  
            <xs:documentation>Time base. Example: TimeBase="1/48000"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfFrames">  
          <xs:annotation>  
            <xs:documentation>number of frames</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="StartTime" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track start time. Example: StartTime="PT2.669S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="Duration" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track duration. Example: Duration="PT25M37.757S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="VideoTrackType">  
        <xs:annotation>  
          <xs:documentation>A specific video track in hello parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="FourCC" type="xs:string" use="required">  
              <xs:annotation>  
                <xs:documentation>video codec FourCC code</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Profile" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>profile</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Level" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>level</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="PixelFormat" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>Video track's pixel format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Width" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video width in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Height" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video height in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioNumerator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioDenominator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioNumerator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioDenominator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="FrameRate" use="required">  
              <xs:annotation>  
                <xs:documentation>measured video frame rate in .3f format</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:decimal">  
                  <xs:minInclusive value="0"/>  
                  <xs:fractionDigits value="3"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average video bit rate in kilobits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="MaxGOPBitrate">  
              <xs:annotation>  
                <xs:documentation>Max GOP average bitrate for this video track, in kilobits per second</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="HasBFrames" type="xs:int">  
              <xs:annotation>  
                <xs:documentation>video track number of B frames</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:complexType name="AudioTrackType">  
        <xs:annotation>  
          <xs:documentation>a specific audio track in hello parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="SampleFormat"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>sample format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="ChannelLayout"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>channel layout</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Channels" use="required">  
              <xs:annotation>  
                <xs:documentation>number of audio channels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SamplingRate" use="required">  
              <xs:annotation>  
                <xs:documentation>audio sampling rate in samples/sec or Hz</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average audio bit rate in bits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="BitsPerSample">  
              <xs:annotation>  
                <xs:documentation>Bits per sample for hello wFormatTag format type</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:element name="AssetFiles">  
        <xs:annotation>  
          <xs:documentation>Collection of AssetFile entries for hello encoding job</xs:documentation>  
        </xs:annotation>  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="AssetFile" minOccurs="1" maxOccurs="unbounded">  
              <xs:annotation>  
                <xs:documentation>asset file</xs:documentation>  
              </xs:annotation>  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="Programs" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>This is hello collection of all programs when file is MPEG-TS</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Program" type="ProgramType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is hello collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" type="VideoTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is hello collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" type="AudioTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded" />  
                </xs:sequence>  
                <xs:attribute name="Name" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>hello media asset file name</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="Size" use="required">  
                  <xs:annotation>  
                    <xs:documentation>size of file in bytes</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:long">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
                <xs:attribute name="Duration" type="xs:duration" use="required">  
                  <xs:annotation>  
                    <xs:documentation>content play back duration. Example: Duration="PT25M37.757S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="NumberOfStreams" type="xs:int" use="required">  
                  <xs:annotation>  
                    <xs:documentation>number of streams in asset file</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatNames" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatVerboseName" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format verbose names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="StartTime" type="xs:duration">  
                  <xs:annotation>  
                    <xs:documentation>content start time. Example: StartTime="PT2.669S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="OverallBitRate">  
                  <xs:annotation>  
                    <xs:documentation>average bitrate of hello asset file in kbps</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:int">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:schema>  


## <a name="xml"></a> XML 예제
hello 다음은 hello 입력 메타 데이터 파일의 예입니다.  

    <?xml version="1.0" encoding="utf-8"?>  
    <AssetFiles xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata">  
      <AssetFile Name="bear.mp4" Size="1973733" Duration="PT12.678S" NumberOfStreams="2" FormatNames="mov,mp4,m4a,3gp,3g2,mj2" FormatVerboseName="QuickTime / MOV" StartTime="PT0S" OverallBitRate="1245">  
        <VideoTracks>  
          <VideoTrack Id="1" Codec="h264" CodecLongName="H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10" TimeBase="1/29970" NumberOfFrames="375" StartTime="PT0.034S" Duration="PT12.645S" FourCC="avc1" Profile="High" Level="4.1" PixelFormat="yuv420p" Width="512" Height="384" DisplayAspectRatioNumerator="4" DisplayAspectRatioDenominator="3" SampleAspectRatioNumerator="1" SampleAspectRatioDenominator="1" FrameRate="29.656" Bitrate="1043" HasBFrames="1">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Video Media Handler" />  
          </VideoTrack>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="aac" CodecLongName="AAC (Advanced Audio Coding)" TimeBase="1/44100" NumberOfFrames="546" StartTime="PT0S" Duration="PT12.678S" SampleFormat="fltp" ChannelLayout="stereo" Channels="2" SamplingRate="44100" Bitrate="156" BitsPerSample="0">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Sound Media Handler" />  
          </AudioTrack>  
        </AudioTracks>  
        <Metadata key="major_brand" value="mp42" />  
        <Metadata key="minor_version" value="0" />  
        <Metadata key="compatible_brands" value="mp42mp41" />  
        <Metadata key="creation_time" value="2010-03-10 16:11:53" />  
        <Metadata key="comment" value="Courtesy of National Geographic.  Used by Permission." />  
      </AssetFile>  
    </AssetFiles>  

## <a name="next-steps"></a>다음 단계
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

