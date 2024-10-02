---
layout: post
title: 노마드코더 React Native 101
date: 2024-08-24
description: Making React Native applications with Expo
tags: react-native application
categories: study
giscus_comments: true
related_posts: false
toc:
  sidebar: left
---

# React Native

## React Native 작동원리
- translator : interface btw ios, android and us
- send message to ios or android
  - not browser!
- JavaScript 코드만 작성하면 알아서 통역해줌!
  - 메세지를 수신하고 발신하는 곳 = 자바스크립트
- 자바스크립트 - bridge - operating system

## The Rules of native
- React Native 는 Web 스타일을 따르지 않음!
  - div, span, p ... 사용 X
  - StyleSheet.create 을 사용해서 object를 만들면 auto complete 기능 사용가능!
  - component는 App() 에 담는다
  - StatusBar는 Text 아래에 위치하는게 X

## React Native Component
- [reactnative.dev/docs](https://reactnative.dev/docs/getting-started)
- 기본적으로 개발자에게 많은 기능을 제공하려고했으나 할 일이 너무 많아짐, 불가능해짐
  - 지원 범위를 줄임 => 쉽게 유지 보수 & 초 빠르게 만들기 위해 & 자체 component, API를 쉽게 사용하도록
    - Navigation, AsyncStorage ... deprecated!
    - community 에서 deprecated 기능 사용 가능!
      - but, bug 발생시 빠른 조치가 불가능할수도 있음
- Expo SDK : 엄청나게 멋진 packages / API 찾을수 있음!

### component vs API
- component : 화면에 Rendering 되는것
- API : JavaScript 코드(os와 연결시키는 역할)

### TouchableOpacity
- sort of View(Box) that is ready to listen event



## Layout
- defalut flexbox : column
- width, height X -> use 'proportion'
  - parent flex가 있어야 children flex가 존재!

## Expo command
1. Start project
  - `npx create-expo-app {project name} --template blank`
    - {}에 project name 입력
    - template, blank 버전으로 생성

## Trouble Shooting
### `xcrun: error: unable to find utility "simctl", not a developer tool or in PATH`
- xcode - settings - locations - command line tool
- 아마 버전 정보가 나와서 잘 선택되었다고 생각할수도 있지만 자세히 보면 아래 연한 회색 글자에 위치 설저이 안되있는걸 볼수 있음
- 버전을 한번 눌러주면 이제 주소가 제대로 설정됨

- `xcrun simctl list` 해서 제대로 설정되었는지 확인
