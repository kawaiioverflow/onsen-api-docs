# onsen-api-docs

onsen-api-docs は[インターネットラジオステーション＜音泉＞](https://www.onsen.ag/)の API の非公式なドキュメントです。

## 目次

- [注意事項](#注意事項)
- [App API](#app-api)
- [Web API](#web-api)

## 注意事項

サードパーティで使うことを想定した API ではないため、実際にリクエストを送ることは、推奨しません。 リクエストを送る場合は、**自己責任**でお願いします。

## App API

主にアプリから利用されることを想定した API です。

### ベース URI

```
https://app.onsen.ag
```

### 認証

一部のエンドポイントでは、トークンが必要です。

その場合は、事前に[トークンを取得する](#app-post-oauth-token)エンドポイントで取得したトークンを、`Authorization` ヘッダに指定して、リクエストします。

### エンドポイント一覧

| 概要                                             | メソッド | パス                            | 認証               |
| :----------------------------------------------- | :------- | :------------------------------ | :----------------- |
| [認可コードを取得する](#app-get-oauth-authorize) | `GET`    | `/oauth/authorize`              |                    |
| [トークンを取得する](#app-post-oauth-token)      | `POST`   | `/oauth/token`                  |                    |
| 番組一覧を取得する                               | `GET`    | `/api/programs`                 |                    |
| 番組詳細を取得する                               | `GET`    | `/api/programs/:directory_name` |                    |
| アカウント詳細を取得する                         | `GET`    | `/api/me`                       | :heavy_check_mark: |

<h4 id="app-get-oauth-authorize"><code>GET /oauth/authorize</code></h4>

このエンドポイントにアクセスして、サインインすることで、認可コードを取得することができます。

##### パラメータ

| 種類   | 名称            | 内容                                                               | 必須               |
| :----- | :-------------- | :----------------------------------------------------------------- | :----------------- |
| クエリ | `client_id`     | `b3d68e56145a5d085f6b0ecc6e1ad4a83345ff4ce97d3e16ace95208ad2f1d2f` | :heavy_check_mark: |
| クエリ | `redirect_uri`  | `ag.onsen.app://oauth2callback`                                    | :heavy_check_mark: |
| クエリ | `response_type` | `code`                                                             | :heavy_check_mark: |
| クエリ | `scope`         | `private`                                                          | :heavy_check_mark: |

##### 例

```
GET https://app.onsen.ag/oauth/authorize?client_id=b3d68e56145a5d085f6b0ecc6e1ad4a83345ff4ce97d3e16ace95208ad2f1d2f&redirect_uri=ag.onsen.app://oauth2callback&response_type=code&scope=private
```

上記 URL にアクセスして、自身のアカウントでサインインする。 `ag.onsen.app://oauth2callback?code=` のような URL にリダイレクトされるため、`?code=` のあとの文字列（認可コード）を取得する。

<h4 id="app-post-oauth-token"><code>POST /oauth/token</code></h4>

アクセストークンを取得することができます。

##### パラメータ

| 種類   | 名称            | 内容                                                               | 必須               |
| :----- | :-------------- | :----------------------------------------------------------------- | :----------------- |
| ヘッダ | `Content-Type`  | `application/x-www-form-urlencoded`                                | :heavy_check_mark: |
| 本文   | `client_id`     | `b3d68e56145a5d085f6b0ecc6e1ad4a83345ff4ce97d3e16ace95208ad2f1d2f` | :heavy_check_mark: |
| 本文   | `client_secret` | `291ba633343212ad706abbb4dae8cda6aa96ae53ed6597298121e63db491a089` | :heavy_check_mark: |
| 本文   | `grant_type`    | `authorization_code`                                               | :heavy_check_mark: |
| 本文   | `code`          | `private`                                                          | :heavy_check_mark: |
| 本文   | `redirect_uri`  | `ag.onsen.app://oauth2callback`                                    | :heavy_check_mark: |

##### 例

```
POST https://app.onsen.ag/oauth/token
```

## Web API

主に公式サイトから利用されることを想定した API です。

### ベース URI

```
https://www.onsen.ag
```

### 認証

一部のエンドポイントでは、トークンが必要です。

その場合は、事前にサインインするエンドポイントへのリクエストで取得した Cookie を使用して、リクエストします。

### エンドポイント一覧

| 概要                                              | メソッド | パス                                 | 認証               |
| :------------------------------------------------ | :------- | :----------------------------------- | :----------------- |
| サインインする                                    | `POST`   | `/web_api/signin`                    |                    |
| イベント記事一覧を取得する                        | `GET`    | `/web_api/event_articles`            |                    |
| オススメ記事一覧を取得する                        | `GET`    | `/web_api/recommended_articles`      |                    |
| 広告一覧を取得する                                | `GET`    | `/web_api/commercials`               |                    |
| バナー一覧を取得する                              | `GET`    | `/web_api/ads/default`               |                    |
| 変更履歴一覧を取得する                            | `GET`    | `/web_api/change_logs`               |                    |
| 番組一覧を取得する                                | `GET`    | `/web_api/programs`                  |                    |
| 番組詳細を取得する                                | `GET`    | `/web_api/programs/:directory_name`  |                    |
| オススメ番組一覧を取得する                        | `GET`    | `/web_api/programs/recommended`      |                    |
| 番組別声優一覧を取得する                          | `GET`    | `/web_api/programs/performers`       |                    |
| 番組を検索する                                    | `GET`    | `/web_api/programs/search`           |                    |
| 声優を検索する                                    | `GET`    | `/web_api/programs/search_performer` |                    |
| アニラジアワード 音泉ノミネート番組一覧を取得する | `GET`    | `/web_api/rankings`                  |                    |
| アカウント詳細を取得する                          | `GET`    | `/web_api/me`                        | :heavy_check_mark: |
