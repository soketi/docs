# 🔐 SSL Configuration

SSL support is included with soketi by default. If one of the following [environment variables](environment-variables.md) is set, the server will start using SSL instead of plain HTTP.

### Environment Variables

| Name       | Default | Possible values | Description                                     |
| ---------- | ------- | --------------- | ----------------------------------------------- |
| `SSL_CERT` | `''`    | File paths      | The path to the SSL certificate file.           |
| `SSL_KEY`  | `''`    | File paths      | The path to the SSL key file.                   |
| `SSL_PASS` | `''`    | String          | The passphrase (if any) for the SSL key         |
| `SSL_CA`   | `''`    | File paths      | The path to the SSL Certificate Authority file. |
