---
link: https://springfall.cc/article/2025-01/mac-settings
byline: 김태훈
site: 김태훈
date: 2025-01-10T09:00
slurped: 2025-03-15T21:05
title: 개발자 MacBook 종합 세팅 - 2025년 버전
---

## 목차

- [초기화](https://springfall.cc/article/2025-01/mac-settings#%EC%B4%88%EA%B8%B0%ED%99%94)
- [맥북 업데이트](https://springfall.cc/article/2025-01/mac-settings#%EB%A7%A5%EB%B6%81-%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8)
- [시스템 설정](https://springfall.cc/article/2025-01/mac-settings#%EC%8B%9C%EC%8A%A4%ED%85%9C-%EC%84%A4%EC%A0%95)
- [기초 프로그램 설치](https://springfall.cc/article/2025-01/mac-settings#%EA%B8%B0%EC%B4%88-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%A8-%EC%84%A4%EC%B9%98)
    - [Google Chrome: 웹 브라우저](https://springfall.cc/article/2025-01/mac-settings#google-chrome-%EC%9B%B9-%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80)
    - [Bitwarden: 비밀번호 관리자](https://springfall.cc/article/2025-01/mac-settings#bitwarden-%EB%B9%84%EB%B0%80%EB%B2%88%ED%98%B8-%EA%B4%80%EB%A6%AC%EC%9E%90)
    - [Raycast: Spotlight 대체 + 부가기능](https://springfall.cc/article/2025-01/mac-settings#raycast-spotlight-%EB%8C%80%EC%B2%B4--%EB%B6%80%EA%B0%80%EA%B8%B0%EB%8A%A5)
- [Finder에서 모든 파일 확장자 보기](https://springfall.cc/article/2025-01/mac-settings#finder%EC%97%90%EC%84%9C-%EB%AA%A8%EB%93%A0-%ED%8C%8C%EC%9D%BC-%ED%99%95%EC%9E%A5%EC%9E%90-%EB%B3%B4%EA%B8%B0)
- [업무용 및 개인 프로그램 설치](https://springfall.cc/article/2025-01/mac-settings#%EC%97%85%EB%AC%B4%EC%9A%A9-%EB%B0%8F-%EA%B0%9C%EC%9D%B8-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%A8-%EC%84%A4%EC%B9%98)
- [iTerm2](https://springfall.cc/article/2025-01/mac-settings#iterm2)
- [oh-my-zsh](https://springfall.cc/article/2025-01/mac-settings#oh-my-zsh)
- [Homebrew: 패키지 매니저](https://springfall.cc/article/2025-01/mac-settings#homebrew-%ED%8C%A8%ED%82%A4%EC%A7%80-%EB%A7%A4%EB%8B%88%EC%A0%80)
    - [Xcode Command line tools](https://springfall.cc/article/2025-01/mac-settings#xcode-command-line-tools)
- [zplug: zsh 플러그인 설치](https://springfall.cc/article/2025-01/mac-settings#zplug-zsh-%ED%94%8C%EB%9F%AC%EA%B7%B8%EC%9D%B8-%EC%84%A4%EC%B9%98)
- [Amazon Q: 터미널 자동완성 프로그램](https://springfall.cc/article/2025-01/mac-settings#amazon-q-%ED%84%B0%EB%AF%B8%EB%84%90-%EC%9E%90%EB%8F%99%EC%99%84%EC%84%B1-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%A8)
- [Powerlevel10k: 터미널 테마](https://springfall.cc/article/2025-01/mac-settings#powerlevel10k-%ED%84%B0%EB%AF%B8%EB%84%90-%ED%85%8C%EB%A7%88)
- [GitHub](https://springfall.cc/article/2025-01/mac-settings#github)
- [Git](https://springfall.cc/article/2025-01/mac-settings#git)
- [asdf: The Multiple Runtime Version Manager](https://springfall.cc/article/2025-01/mac-settings#asdf-the-multiple-runtime-version-manager)
- [fzf: general-purpose command-line fuzzy finder](https://springfall.cc/article/2025-01/mac-settings#fzf-general-purpose-command-line-fuzzy-finder)
- [direnv: 폴더 기반 환경변수 설정 (필수 아님)](https://springfall.cc/article/2025-01/mac-settings#direnv-%ED%8F%B4%EB%8D%94-%EA%B8%B0%EB%B0%98-%ED%99%98%EA%B2%BD%EB%B3%80%EC%88%98-%EC%84%A4%EC%A0%95-%ED%95%84%EC%88%98-%EC%95%84%EB%8B%98)
- [Visual Studio Code](https://springfall.cc/article/2025-01/mac-settings#visual-studio-code)
- [`.zshrc` 파일 중간 점검 및 커스텀 명령어 추가](https://springfall.cc/article/2025-01/mac-settings#zshrc-%ED%8C%8C%EC%9D%BC-%EC%A4%91%EA%B0%84-%EC%A0%90%EA%B2%80-%EB%B0%8F-%EC%BB%A4%EC%8A%A4%ED%85%80-%EB%AA%85%EB%A0%B9%EC%96%B4-%EC%B6%94%EA%B0%80)
- [폰트 설치](https://springfall.cc/article/2025-01/mac-settings#%ED%8F%B0%ED%8A%B8-%EC%84%A4%EC%B9%98)
- [기타 프로그램](https://springfall.cc/article/2025-01/mac-settings#%EA%B8%B0%ED%83%80-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%A8)
- [번외](https://springfall.cc/article/2025-01/mac-settings#%EB%B2%88%EC%99%B8)