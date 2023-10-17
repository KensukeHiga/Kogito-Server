# kogito-server

This project uses Quarkus, the Supersonic Subatomic Java Framework.

If you want to learn more about Quarkus, please visit its website: https://quarkus.io/ .

## TODO
- [x] kogitoサービスの起動
- [x] SwaggerUIからの送受信確認
- [ ] dmnを外部サービスで新規作成、更新、削除
- [ ] kubernetes,dockerでのデプロイ
- [ ] ログの設定
- [ ] dmnの更新を無停止で適用する
- [ ] テストコードの作成

## 構築手順
1.ルールファイルがない状態のプロジェクト作成
```
mvn io.quarkus:quarkus-maven-plugin:create -DprojectGroupId=org.acme -DprojectArtifactId=kogito-server -Dextensions="kogito-quarkus,resteasy-reactive-jackson,quarkus-smallrye-openapi,quarkus-smallrye-health"
```
2.依存に不足があったので↓をpomに追加
```
<dependency>
    <groupId>jakarta.ws.rs</groupId>
    <artifactId>jakarta.ws.rs-api</artifactId>
    <version>3.1.0</version>
</dependency>
```
3.データタイプ、ルール作成  
  - 扱うデータ（Asset classなど）を登録する。
  - 登録したデータを利用し入力、出力、条件式を作成する。
  - 参考記事リンク１：https://qiita.com/tomotagwork/items/1a16377d882e3886f69f
  - 参考記事リンク２：https://qiita.com/potstickers/items/48fed74660e396954eed

## Running the application in dev mode

You can run your application in dev mode that enables live coding using:
```shell script
./mvnw compile quarkus:dev
```

> **_NOTE:_**  Quarkus now ships with a Dev UI, which is available in dev mode only at http://localhost:8080/q/dev/.

## SwaggerUIからRESTによるルール呼び出し
上記「Dev UI」から「Swagger UI」に遷移することができる。<br>
あらかじめ、登録されたdmnファイルをもとにエンドポイントが作成されており、そのAPIを呼び出すことができる。

## Packaging and running the application

The application can be packaged using:
```shell script
./mvnw package
```
It produces the `quarkus-run.jar` file in the `target/quarkus-app/` directory.
Be aware that it’s not an _über-jar_ as the dependencies are copied into the `target/quarkus-app/lib/` directory.

The application is now runnable using `java -jar target/quarkus-app/quarkus-run.jar`.

If you want to build an _über-jar_, execute the following command:
```shell script
./mvnw package -Dquarkus.package.type=uber-jar
```

The application, packaged as an _über-jar_, is now runnable using `java -jar target/*-runner.jar`.

## Creating a native executable

You can create a native executable using: 
```shell script
./mvnw package -Dnative
```

Or, if you don't have GraalVM installed, you can run the native executable build in a container using: 
```shell script
./mvnw package -Dnative -Dquarkus.native.container-build=true
```

You can then execute your native executable with: `./target/kogito-server-1.0.0-SNAPSHOT-runner`

If you want to learn more about building native executables, please consult https://quarkus.io/guides/maven-tooling.

## Related Guides

- SmallRye OpenAPI ([guide](https://quarkus.io/guides/openapi-swaggerui)): Document your REST APIs with OpenAPI - comes with Swagger UI
- SmallRye Health ([guide](https://quarkus.io/guides/smallrye-health)): Monitor service health
- Kogito ([guide](https://quarkus.io/version/2.13/guides/kogito)): Add business automation capabilities - processes and rules with Kogito (a toolkit that originates from projects Drools and jBPM)

## Provided Code

### RESTEasy Reactive

Easily start your Reactive RESTful Web Services

[Related guide section...](https://quarkus.io/guides/getting-started-reactive#reactive-jax-rs-resources)

### SmallRye Health

Monitor your application's health using SmallRye Health

[Related guide section...](https://quarkus.io/guides/smallrye-health)
