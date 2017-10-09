엔터프라이즈 솔루션을 사용하여 생성되는 루트 인증서를 사용하거나(권장됨) 자체 서명된 인증서를 생성할 수 있습니다. E-64로 인코딩된 X.509.cer hello 공용 인증서 데이터 (hello 개인 키가 아니라) 내보낼 hello 루트 인증서를 만든 후 파일을 공용 인증서 데이터 tooAzure hello를 업로드 합니다.

* **엔터프라이즈 인증서:** 엔터프라이즈 솔루션을 사용하는 경우 기존 인증서 체인을 사용할 수 있습니다. 원하는 toouse hello 루트 인증서에 대 한 hello.cer 파일을 가져옵니다.
* **자체 서명 된 루트 인증서:** toocreate 자체 서명 된 루트 인증서 인증서 엔터프라이즈 솔루션을 사용 하지 않는 경우 해야 합니다. 아래 P2S hello 인증서 문서 중 하나에 hello 단계를 수행 합니다. 그렇지 않은 경우 만든 hello 인증서 P2S 연결과 호환 되지 않습니다 및 클라이언트 tooconnect 시도할 때 연결 오류가 발생 합니다. hello 단계 hello 문서 다음 중 하나에 호환 되는 인증서를 생성 합니다.

  * [Windows 10 PowerShell 지침](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site.md): 이러한 지침은 Windows 10 및 PowerShell toogenerate 인증서가 필요 합니다. 지 원하는 모든 P2S 클라이언트 hello 루트 인증서에서 생성 되는 클라이언트 인증서를 설치할 수 있습니다.
  * [MakeCert 지침](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site-makecert.md): 액세스 tooa Windows 10 컴퓨터 toouse toogenerate 인증서가 없는 경우 MakeCert를 사용 합니다. MakeCert 더 이상 사용 되지 않지만 MakeCert toogenerate 인증서를 계속 사용할 수 있습니다. 지 원하는 모든 P2S 클라이언트 hello 루트 인증서에서 생성 되는 클라이언트 인증서를 설치할 수 있습니다.
