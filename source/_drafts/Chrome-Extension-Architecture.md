---
title: Chrome Extension Architecture
tags:
  - chrome-extension
---

크롬 extension은 HTML, CSS, JavaScript, images, 그리고 web platform에 쓰이는 파일들을 압축시킨 번들이다.

크롬 extension이 어떤 구조를 가지고 있는지 알아보자.



## Architecture

Architecture는 크게 아래 5개의 component를 가지고 있다.

- Manifest
- Background Script
- UI Elements
- Content Script
- Options Page

### manifest

Extension에서 제일 중요한 파일은 `manifest.json` 파일이다. 이 파일에는 extension에 대한 모든 정보(툴바 icon 이미지, 권한, version, extension name 등)를 보여준다.

굉장히 많은 옵션들이 있는데, 필수와 추천 옵션에 대해서만 자세히 알아보자.

```json
{
  // Required
  "manifest_version": 2,
  "name": "My Extension",
  "version": "versionString",

  // Recommended
  "default_locale": "en",
  "description": "A plain text description",
  "icons": {...},

  // Pick one (or none)
  "browser_action": {...},
  "page_action": {...},

  // Optional
  "action": ...,
  "author": ...,
  "automation": ...,
  "background": {
    // Recommended
    "persistent": false,
    // Optional
    "service_worker":
  },
  "chrome_settings_overrides": {...},
  "chrome_ui_overrides": {
    "bookmarks_ui": {
      "remove_bookmark_shortcut": true,
      "remove_button": true
    }
  },
  "chrome_url_overrides": {...},
  "commands": {...},
  "content_capabilities": ...,
  "content_scripts": [{...}],
  "content_security_policy": "policyString",
  "converted_from_user_script": ...,
  "current_locale": ...,
  "declarative_net_request": ...,
  "devtools_page": "devtools.html",
  "event_rules": [{...}],
  "externally_connectable": {
    "matches": ["*://*.example.com/*"]
  },
  "file_browser_handlers": [...],
  "file_system_provider_capabilities": {
    "configurable": true,
    "multiple_mounts": true,
    "source": "network"
  },
  "homepage_url": "http://path/to/homepage",
  "import": [{"id": "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa"}],
  "incognito": "spanning, split, or not_allowed",
  "input_components": ...,
  "key": "publicKey",
  "minimum_chrome_version": "versionString",
  "nacl_modules": [...],
  "oauth2": ...,
  "offline_enabled": true,
  "omnibox": {
    "keyword": "aString"
  },
  "optional_permissions": ["tabs"],
  "options_page": "options.html",
  "options_ui": {
    "chrome_style": true,
    "page": "options.html"
  },
  "permissions": ["tabs"],
  "platforms": ...,
  "replacement_web_app": ...,
  "requirements": {...},
  "sandbox": [...],
  "short_name": "Short Name",
  "signature": ...,
  "spellcheck": ...,
  "storage": {
    "managed_schema": "schema.json"
  },
  "system_indicator": ...,
  "tts_engine": {...},
  "update_url": "http://path/to/updateInfo.xml",
  "version_name": "aString",
  "web_accessible_resources": [...]
}
```

- `manifest_version` : 
- `name` :
- `version` : 
- `default_locale` : 
- `description` :
- `icons` : 
- `browser_action` : 주소 창 오른 쪽에 항상 보이게 해주는 
- `page_action` : 주소 창 오른 쪽에 선택적으로 보이게 해주는
- `background` : 


### Background Script

Background Script는 extension의 이벤트 핸들러입니다. browser events에 대한 listener를 가지고 있습니다.

[추가로 쓰기]()

참고로 필요할 때만 로드되고, 아닐 땐 로드되지 않는게 효과적인 Background Script입니다.


### UI Elements

UI Page는 HTML 페이지와 JavaScript 로직을 가지고 있는 Component 입니다. 

UI Element는 Background Script와 통신하며 다양한 기능을 구현 할 수도 있습니다. 
[예제](https://developer.chrome.com/extensions/getstarted#user_interface)(`declarative content API`를 이용하여 특정 url에서만 팝업이 활성화 되게 하는 예제입니다.)

![](/image/chrome-extension-architecture/ui-element.png)
[출처 : https://developer.chrome.com/extensions/overview](https://developer.chrome.com/extensions/overview)

### Content Scripts

Content script는 browser에서 로드 될 javascript를 가지고 있습니다.

Content script는 방문한 웹 페이지의 DOM을 읽고 수정 할 수 있습니다.

![](/image/chrome-extension-architecture/content-script-1.png)
[출처 : https://developer.chrome.com/extensions/overview](https://developer.chrome.com/extensions/overview)

또한, extension과 소통하여 값을 저장하거나 메세지를 교환 할 수 있습니다.

![](/image/chrome-extension-architecture/content-script-2.png)
[출처 : https://developer.chrome.com/extensions/overview](https://developer.chrome.com/extensions/overview)


### Options Page

Options Page는 User가 Extension을 Customize 할 수 있는 페이지 입니다.

---
**Reference**
- [https://developer.chrome.com/extensions/overview](https://developer.chrome.com/extensions/overview)
- [https://developer.chrome.com/extensions/manifest](https://developer.chrome.com/extensions/manifest)
- [https://developer.chrome.com/extensions/background_pages](https://developer.chrome.com/extensions/background_pages)