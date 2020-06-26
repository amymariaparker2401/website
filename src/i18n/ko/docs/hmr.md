# 🔥 빠른 모듈 교체\(HMR\)

빠른 모듈 교체\(Hot Module Replacement\)\(이하 HMR\)는 런타임에 페이지 새로고침 없이 모듈을 자동으로 갱신하므로 개발 경험을 향상시킵니다. 작은 변화에 따라 애플리케이션 상태를 계속 유지할 수 있습니다. Parcel HMR 은 JavaScript 와 CSS 애셋 모두를 지원합니다. 프로덕션 모드에서 HMR 은 자동으로 비활성화 됩니다.

파일을 저장하면 Parcel 은 변한 부분을 다시 빌드하고 이에 영향을 받는 모든 실행중인 클라이언트에 새 코드를 보냅니다. 그 후 새 코드는 이전 버전과 교체되고 모든 부모가 함께 다시 평가 됩니다. 이 과정 중 `module.hot` API 를 사용해 훅\(hook\)을 걸수 있습니다. 이를 통해 모듈이 버려질 때, 또는 새 버전이 들어올 때 코드에 알려줄 수 있습니다. [react-hot-loader](https://github.com/gaearon/react-hot-loader)같은 프로젝트는 이 과정에 도움이 되며, Parcel 에 바로 쓸 수 있습니다.

`module.hot.accept` 와 `module.hot.dispose` 두 메소드를 알아 두세요. `module.hot.accept`를 이 모듈이나 이 모듈의 다른 의존 사항이 갱신될 때 실행되는 콜백과 함께 호출합니다. `module.hot.dispose`는 이 모듈이 교체될 때 호출되는 콜백을 받아들입니다.

```javascript
if (module.hot) {
  module.hot.dispose(function() {
    // 모듈이 곧 폐기 됨
  })

  module.hot.accept(function() {
    // 모듈이나 모듈의 의존 사항이 곧 갱신 됨
  })
}
```

## 의존성 자동설치

Parcel 은 의존성 패키지가 필요할때마다 `node_module`에서 맞는 의존성을 찾고, 만약 찾지 못하면 자동으로 `yarn`이나 `npm`을 이용해 의존성 패키지를 설치합니다.\(`yarn.lock` 파일이 있는지 여부로 패키지 매니저 결정\) 이 기능은 개발자로 하여금 의존성 패키지 설치를 위해 Parcel 을 매번 종료하거나 여러개의 터미널을 띄우지 않아도 되게 해줍니다.

이 기능은 오직 _개발모드_\([`serve`](cli.md#serve) 혹은 [`watch`](cli.md#watch) 명령어 사용시\)에서만 동작합니다. 하지만 프로덕션모드\([`build`](cli.md#build) 명령어\)에선 배포도중 발생하는 원치않는 부작용을 방지하기 위해 자동설치가 비활성화 됩니다.

이 기능은 [`--no-autoinstall`](cli.md#disable-autoinstall) 옵션으로 비활성화 할 수 있습니다.

## Safe Write

일부 텍스트 편집기와 IDE 는 `safe write`라고 부르는 기능으로 파일을 복제한 다음 저장할 때 이름을 바꾸는 방식으로 데이터 유실을 방지합니다.

빠른 모듈 교체를 사용할 때 이 기능은 자동 파일 변경 감지를 막아버립니다. `safe write` 기능을 비활성화 하려면 아래 제시된 방법을 사용하세요.

* `Sublime Text 3` 사용자 설정\(user preferences\)에 `atomic_save: "false"` 를 추가하세요.
* `IntelliJ` 설정\(preferences\)에서 "safe write"로 검색해서 찾은 뒤 비활성화 하세요.
* `Vim` 설정에 `:set backupcopy=yes` 를 추가하세요.
* `WebStorm` Preferences &gt; Appearance & Behavior &gt; System Settings 로 가서 `"safe write"`의 체크를 풀어버리세요.

