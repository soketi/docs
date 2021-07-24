# 🔐 SSL Configuration

SSL support comes out-of-the-box with both the HTTP API and the WS Server. If one of the following environment variables is set, the server will start with SSL instead of plain HTTP.

[Learn more about how to set environment variables to your server.](environment-variables.md)

### SSL Settings

Setting one of the following variables will create an SSL version of the app.

| Name | Default | Possible values | Description |
| :--- | :--- | :--- | :--- |
| `SSL_CERT` | `''` | File paths | The path for the SSL certificate file. |
| `SSL_KEY` | `''` | File paths | The path for the SSL key file. |
| `SSL_PASS` | `''` | File path | The passphrase \(if any\) for the SSL key file to decrypt. |

