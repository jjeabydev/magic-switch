# Magic Switch 작업 지침

## 로컬 macOS 앱 설치와 서명

- `CODE_SIGNING_ALLOWED=NO`로 만든 앱 번들을 서명 없이 설치하지 않습니다.
- 설치 전 내장 프레임워크와 실행 파일을 포함한 앱 전체를 서명합니다. Sparkle 등 내장 프레임워크를 복사하거나 수정한 뒤에는 앱 번들을 다시 서명합니다.
- 사용 가능한 Apple 개발자 인증서가 있으면 같은 인증서로 계속 서명해 macOS 권한 식별자가 바뀌지 않도록 합니다. 임시 서명만 가능한 경우 Bluetooth 권한을 다시 허용해야 할 수 있음을 알립니다.
- 최종 설치 경로의 앱에 `codesign --verify --deep --strict --verbose=2`를 실행합니다. `codesign -dv --verbose=4`로 Bundle ID, Team ID와 서명 주체도 확인합니다. 서명 후 앱 번들을 변경했다면 다시 서명하고 검증합니다.
- Bluetooth 오류를 진단할 때 권한 거부와 라디오 전원 꺼짐을 구분합니다. CoreBluetooth 상태의 `.unauthorized`와 `.poweredOff`를 따로 확인하고, 서명·TCC 접근 실패를 “Bluetooth is off”로 표시하지 않습니다.
- 설치 뒤 앱이 이미 실행 중이면 정상 종료 후 다시 열어 새 실행 파일이 사용되도록 안내합니다.
