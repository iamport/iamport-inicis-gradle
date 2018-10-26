# iamport-inicis-gradle
KG이니시스 결제연동을 위한 아임포트 안드로이드 샘플프로젝트입니다( Gradle )


## 주의사항  

### 1. Mixed Content 허용  

PG사 결제화면 및 카드사 인증화면간 여러 번 리디렉션 되는 과정에서 https, http 간 이동이 발생될 수 있습니다. 때문에 결제프로세스가 진행되는 웹뷰 설정을 위해 아래 소스코드 추가를 해주셔야 합니다.   

```java
if (android.os.Build.VERSION.SDK_INT >= Build.VERSION_CODES.LOLLIPOP) {
	settings.setMixedContentMode(WebSettings.MIXED_CONTENT_ALWAYS_ALLOW);
}
```
참고 : [https://github.com/iamport/iamport-inicis-gradle/blob/master/app/src/main/java/com/siot/inicissample/MainActivity.java#L32](https://github.com/iamport/iamport-inicis-gradle/blob/master/app/src/main/java/com/siot/inicissample/MainActivity.java#L32)

### 2. Cookie 허용  

카드사 인증단계에 있어서 브라우저의 쿠키기능을 활용하는 경우들이 있습니다. 결제프로세스가 진행되는 웹뷰에 쿠키허용설정이 되어있어야하며, 허용되어있지 않은 상태에서는 카드사 화면에서 보안키보드가 출력되지 않거나 카드사 화면이 하얗게 출력되는 문제가 발생될 수 있습니다.  

```java
if (android.os.Build.VERSION.SDK_INT >= Build.VERSION_CODES.LOLLIPOP) {
	CookieManager cookieManager = CookieManager.getInstance();
	cookieManager.setAcceptCookie(true);
	cookieManager.setAcceptThirdPartyCookies(mainWebView, true);
}
```

참고 : [https://github.com/iamport/iamport-inicis-gradle/blob/master/app/src/main/java/com/siot/inicissample/MainActivity.java#L31-L35](https://github.com/iamport/iamport-inicis-gradle/blob/master/app/src/main/java/com/siot/inicissample/MainActivity.java#L31-L35)
