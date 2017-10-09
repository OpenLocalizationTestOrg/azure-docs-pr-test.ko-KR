보낸 사람 정책 프레임 워크 (SPF) 레코드가 사용 되는 toospecifying 전자 메일 서버를 지정된 된 도메인 이름의 대신 하 여 전자 메일 toosend 허용 됩니다.  올바른 SPF 레코드의 구성은 중요 tooprevent 받는 사람에 게 전자 메일 '정크 메일'로 표시 합니다.

hello DNS Rfc의이 시나리오를 새 'SPF' 레코드 종류 toosupport를 원래 도입 되었습니다. 이전 이름 서버 toosupport은 또한 허용 hello TXT 레코드 종류 toospecify SPF 레코드의 hello 사용.  이러한 모호성으로이 인해 초래한에 의해 확인 된 tooconfusion [RFC 7208](http://tools.ietf.org/html/rfc7208#section-3.1)합니다.  Hello TXT 레코드 종류를 사용 하 여 SPF 레코드 만든만 해야 하 고 해당 hello SPF 레코드 종류는 사용 되지 않습니다. 상태입니다.

**Azure DNS에서 지 원하는 및 hello TXT 레코드 종류를 사용 하 여 만들어야 하는 SPF 기록 합니다.** hello 사용 되지 않는 SPF 레코드 종류는 지원 되지 않습니다. 때 [DNS 영역 파일을 가져와](../articles/dns/dns-import-export.md), SPF hello 레코드 종류를 사용 하 여 모든 SPF 레코드 변환 됩니다 toohello TXT 레코드 종류입니다.
