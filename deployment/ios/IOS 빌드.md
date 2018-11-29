## IOS 배포

### 필요한것
  1. certificate (development, distribution용 1개씩)
  2. provisioning profile (development, distribution)
 

### 1. ionic cordova build ios (에러나도 상관없음)
  
### 2. project_root/platforms/ios/PROJECT_NAME.xcodeproj 실행
  - version, signing 확인
  - PROJECT_NAME -> Generic iOS Device 인 상태에서 상단메뉴 Product -> Archive
  - 완료후 나오는 화면에서(Window -> Organizer로도 실행가능) Distribute App
  - iOS App Store -> Upload, Export (둘다 상관없음)
    - 옴니스피아노의 경우 Upload 에러가 있어 Export 한 후에 Application loader로 앱스토어 업로드
    
### 3. appstoreconnect.apple.com
  - 활동내역에서 올린 ipa 확인 후 처리완료되면 
