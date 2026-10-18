# POS-TEST-BE

簡易POSアプリのバックエンド(FastAPI)。Azure App Service(Linux / Python 3.12)へGitHub Actionsでデプロイする。

## Azure App Service の設定

スタートアップコマンド:

```
python -m uvicorn app.main:app --host 0.0.0.0 --port 8000
```

アプリケーション設定(環境変数):

| 名前 | 値 |
|---|---|
| `ENV` | `production`(Swagger/ReDocを無効化) |
| `DATABASE_URL` | `mysql+pymysql://<user>:<password>@<host>:3306/<dbname>` |
| `JWT_SECRET_KEY` | 32バイト以上のランダム文字列 |
| `CORS_ALLOW_ORIGINS` | `["https://<フロントエンドのホスト名>"]` |
| `SCM_DO_BUILD_DURING_DEPLOYMENT` | `true` |

DBスキーマの作成(`alembic upgrade head`)と初期管理者の投入(`scripts/seed_initial_admin.py`)は
デプロイとは別に一度だけ実行する。
