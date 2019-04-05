---
layout: post
title: "Swift5 사용함으로써 예방할 수 있는 보안 취약점"
---

얼마 전 Swift5가 릴리즈 되었고 변경점을 보다 떠오른 생각을 적어본다.

> #### New Features
>
> - Swift apps no longer include dynamically linked libraries for the Swift standard library and Swift SDK overlays in build variants for devices running iOS 12.2, watchOS 5.2, and tvOS 12.2. As a result, Swift apps can be smaller when they’re shipped in the App Store, deployed for testing using TestFlight, or thinned in an app archive for local development distribution.

**Swift 5로 개발된 앱은  iOS 12.2부터는 동적 링크 라이브러리가 포함되지 않는다는 것이다.**

이 점에서 예방할 수 있는 보안 취약점은 바로 코드 인젝션을 통한 해킹을 방지할 수 있다는 것이다. 기존 앱들은 ipa 파일 안에 `Dylibs`라는 폴더를 가지고 있고 안에는 동적 링크 라이브러리 파일들이 존재하는데 이를 이용하여 해커가 원하는 코드를 앱에 주입하여 악용할 수 있기 때문이다.



---

​    

  

 때는 2016년 여름  X켓몬Go가 유행하던 때 우리나라에서는 X켓몬Go가 서비스되지 않지만 속초에서는 X켓몬을 잡을 수 있어서 사람들은 속초로 여행갔었고 이후 정식 서비스가 되었을 때 우리나라에 X켓몬이 유행을 했었다. 물론 우리 회사에서도 유행했었기 때문에, 우리 팀에서도 X켓몬Go를 즐기고 있었다. 

 여기서 바로 iOS와 안드로이드 사용자가의 차이가 발생하였다. 안드로이드 디바이스에서 Fake GPS 앱을 받는 것만으로 GPS를 조작하여 원하는 위치로 이동하여 등장하는 X나뇽을 잡을 수 있었다는 것이다. 이때 팀에서 iOS 개발자로 일하고 있었던 나와 사수분은 안드로이드 기기가 없어 점심시간마다 안드로이드 개발자 분들이 X나뇽 잡고 있던걸 구경만 하고 있었다.

 이 당시 나는  iOS에서 다른 앱에서 다른 앱의 GPS를 조작하거나 앱을 통해 시스템의 GPS를 조작하는 것이 불가능한 것으로 알고 있었다. 지금도 그런 것으로 알고 있다. ~~하지만 우리는 답 찾을 것이다. 언제나 그래 왔듯이~~ 

그래서 나는 주말에 다른 방법이 없는 것인지 구글링을 하다  이 [포스트](https://medium.com/@kennethpoon/how-to-perform-ios-code-injection-on-ipa-files-1ba91d9438db)를 보게 되었다.

이 [깃허브](https://github.com/depoon/iOSDylibInjectionDemo)에 나오는 내용에 따르면 메소드 스위즐링과 동적 링크 라이브러리를 바꿔치기 함으로써 코드 인젝션과  GPS 스푸핑이 가능 하다는 것이다. 

```
1. ipa 파일을 구한다.
2. 예제를 보고 iOS 다이나믹 프레임워크를 빌드한다.
3. 더 이상 자세한 내용은 생략한다.
4. 쉘 스크립트를 사용하여 ipa를 패치한다.
5. 시디아 임팩터를 사용하여 사이닝하여 기기에 설치한다.
```

 이 과정을 진행하면서 개발자라면 중간에 기존 앱의 윈도우를 하이젝킹하여 원하는 UI를 만들어 여러 기능을 추가할 수 있고, 이는 여러 가지 방법으로 악용될 수 있는 것으로 보였다. 원하는 GPS 좌표를 입력하여 X나뇽을 잡는다던지 말이다.

 하지만 iOS12.2부터 Swift5로 개발된 앱은 동적 링크 라이브러리를 포함하지 않으므로 위와 같은 방식에 해킹하는 것은 불가능할 것이라는 생각이 들었다. 앱의 용량 자체가 줄어드는 것도 좋지만 위와 같은 해킹 방식 자체가 원천적으로 차단된 것이니 조금 더 앱이 안전해진다고 생각한다.
