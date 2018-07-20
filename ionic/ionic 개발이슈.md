
# Ionic 개발이슈

### 안드로이드 & Ios UI 통일

~~~typescript
/** app.module.ts **/
  imports: [
    IonicModule.forRoot(MyApp, {
      mode: 'ios',
    }),
  ]
/** mode를 'md'로 하는 경우에는 안드로이드 기준 UI 통일  **/
~~~

### Compnent 사용하기

1. 생성 명령어
~~~
ionic g component component-name
~~~

2. module화
~~~typescript
@NgModule({
  declarations: [
    DetailComponent,
    GridComponent,
    BarComponent,
    ListComponent,
    MapComponent,
  ],
  imports: [
    IonicModule
  ],
  exports: [
    DetailComponent,
    GridComponent,
    BarComponent,
    ListComponent,
    MapComponent,
  ],
})

export class ComponentsModule {}
~~~

3. 사용될 page의 module에 추가하기

~~~typescript
@NgModule({
  declarations: [
    EntryPage,
  ],
  imports: [
    IonicPageModule.forChild(EntryPage),
    ComponentsModule,
  ],
  entryComponents: [
    EntryPage,
  ]
})
export class EntryPageModule {}
~~~

### Ionic Page & Lazy Loading

https://ionicacademy.com/ionic-3-lazy-loading/

*Issues
  - Ionic Page 구현시 ionic serve로 브라우저단 테스트중 코드 수정을 하면 Tabs가 사라지는 버그가 있다.
  - 해당 경우 tabs자체도 page화 시켜주면 된다.
  

### Angular HTTP Intercepter

https://medium.com/@ryanchenkie_40935/angular-authentication-using-the-http-client-and-http-interceptors-2f9d1540eb8

~~~typescript
/** example code **/
/** token.interceptor.ts **/
@Injectable()
export class AuthenticationInterceptor implements HttpInterceptor {
  constructor(public auth: AuthService) {
  }

  intercept(request: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {

    if (!!this.auth.getToken()) {
      request = request.clone({
        setHeaders: {
          'Content-Type': 'application/json',
          Authorization: 'Token ' + this.auth.getToken(),
        }
      });
    }
    else {
      request = request.clone({
        setHeaders: {
          'Content-Type': 'application/json',
        }
      });
    }

    return next.handle(request);
  }
}

export const httpProvider = {provide: HTTP_INTERCEPTORS, useClass: AuthenticationInterceptor, multi: true};

/** app.module.ts **/
@NgModule({
  declarations: [
    MyApp,
  ],
  imports: [
    BrowserModule,
    IonicModule.forRoot(MyApp),
    HttpClientModule,
  ],
  bootstrap: [IonicApp],
  entryComponents: [
    MyApp,
  ],
  providers: [
    StatusBar,
    SplashScreen,
    {provide: ErrorHandler, useClass: IonicErrorHandler},
    httpProvider,
  ]
})
~~~


### Error: Module parse failed: Unterminated string constant
\u2028 이라는 zero-width 문자로 인한 에러

Zero Width Characters locator 설치후 해당 문자 제거하면 오류해결
