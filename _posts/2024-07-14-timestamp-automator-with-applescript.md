---
layout: post
title: 맥OS에서 applescript를 활용해 타임스탬프 단축키로 추가하기
date: 2024-07-14
description: 맥에서 단축키로 타임스탬프 추가하는 방법
tags: mac automator applescript timestamp
categories: playing
giscus_comments: true
related_posts: false
toc:
  sidebar: left
---

# 단축키로 간단하게 타임스탬프 추가하기!

[Obsidian](https://obsidian.md/)을 사용하면서 하나의 노트에 내용을 이어서 추가하는 경우 작업하는 순간의 날짜와 시간을 기록하는 습관이 생겼다. 작업 날짜별로 노트를 관리하는게 아니라 주제별로 노트를 관리하다보니 생긴 습관인데, 매번 지금의 날짜와 시간을 확인하고 일일이 추가하는게 번거롭다. <br>
Alfred의 Workflows 기능을 사용해서 쉽게 단축키로 타임스탬프를 추가하면 좋겠지만 Powerpack 유료 기능이기 때문에 맥의 Automator에서 applescript를 활용해 동일한 기능을 구현하는 방법을 찾았다.

## 1. Automator 설정
- Automator 어플리케이션 실행 (spotlight로 검색!)
- New Documnet > type : Quick Action<br>
  ![1 new_document](https://github.com/user-attachments/assets/92e5ff06-e294-451f-8ab9-48bcb6bcabab){: width="60%"}
  ![2 type_quick_action](https://github.com/user-attachments/assets/ba1d11de-16c8-4bcc-94d2-0f0b2f26d736){: width="90%"}
- 'Run AppleScript' 액션을 검색후 선택(더블클릭)<br>
  ![3 find_run_applescript](https://github.com/user-attachments/assets/2e68af1b-15d7-44f0-a2d1-e278bbfd2981){: width="90%"}
- 아래 script 작성
  ```applescript
  -- Insert formatted Date and Time into your documents
  set dateString to do shell script "date +'%Y-%m-%d %A, %H:%M:%'S"
  set the clipboard to dateString

  tell application "System Events"
    set frontmostApplication to name of the first process whose frontmost is true
  end tell

  tell application frontmostApplication
    activate
    tell application "System Events"
      keystroke "v" using {command down}
    end tell
  end tell
  ```
- 나머지 설정은 아래 사진과 동일하게 선택하고 'Run' 버튼으로 실행해서 오류 없는지 확인<br>
  ![4 write_script_and_run](https://github.com/user-attachments/assets/919336a0-7037-4812-9013-a2fb0729a662){: width="90%"}
- Quick Action 저장

## 2. 키보드 단축키 설정
- Settings > Keyboard > Keyboard Shortcuts > Services 
- General > 위에서 저장한 'Automator action' 체크 > 단축키 설정
  - 단축키는 기존 시스템 혹은 다른 어플리케이션 단축키와 겹치지 않는 **고유한 단축키**로 설정<br>
  ![5 set_keyboard_shorcut](https://github.com/user-attachments/assets/f5c0ffda-09ab-4d66-944d-402d35ae55b4){: width="80%"}
  
## 3. Quick Action 사용할 어플리케이션 권한 설정
- Settings > Privacy & Security > Accessibillity 
- Quick Action을 사용할 어플리케이션 선택해서 권한 추가<br>
  ![6 set_accessibility](https://github.com/user-attachments/assets/b20cfc4f-21de-4433-8693-91708fac6ca4){: width="80%"}

## 4. 단축키로 타임스탬프 추가
- `2024-07-14 Sunday, 22:54`

### 4-2. 타임스탬프 추가 ver2
- Obsidian과 노트에서는 위 스크립트로 잘 사용되는데, 웹브라우저와 VScode에서는 실행이 안되는 문제가 있다. 아마도 스크립트 문제인것 같지만 AppleScript를 깊게 파고들기엔 어려운것 같아 claude 도움으로 타임스탬프를 **클립보드에 복사한 뒤에 붙여넣기** 하는 방식의 스크립트를 추가로 만들었다.
  ```AppleScript
  -- Create and copy formatted Date and Time
  set dateString to do shell script "date +'%Y-%m-%d %A, %H:%M'"
  set the clipboard to dateString
  ```
- 동일한 과정으로 진행후 단축키 실행한 후에 붙여넣기(command+v)를 하면 `2024-07-14 Sunday, 22:59` 타임스탬프를 만들수 있다!
  - 이 방식으로는 별도의 애플리케이션 권한 설정이 필요없다:)


## 참고 자료
  - [blog URBANBUSAN](https://urbanbusan.tistory.com/entry/%EB%A7%A5OS-%EC%97%90%EC%84%9C-%ED%98%84%EC%9E%AC-%EC%8B%9C%EA%B0%84%EB%82%A0%EC%A7%9C-%EC%82%BD%EC%9E%85%ED%95%98%EB%8A%94-%EB%8B%A8%EC%B6%95%ED%82%A4-%EC%82%AC%EC%9A%A9)
  - [sixhat.net](https://www.sixhat.net/applescript-insert-date-and-time-into-your-documents.html)
  - [apple community](https://discussions.apple.com/thread/253547282?sortBy=best)
  - [Claude](https://claude.ai/)
