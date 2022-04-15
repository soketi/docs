# 🔐 SSL Configuration

SSL support is included with soketi by default. If one of the following [environment variables](environment-variables.md) is set, the server will start using SSL instead of plain HTTP.

### Environment Variables

| Name               | Default | Possible values | Description                             |
| ------------------ | ------- | --------------- | --------------------------------------- |
| `SOKETI_ISSL_CERT` | `''`    | File paths      | The path to the SSL certificate file.   |
| `SOKETI_SSL_KEY`   | `''`    | File paths      | The path to the SSL key file.           |
| `SOKETI_SSL_PASS`  | `''`    | File path       | The passphrase (if any) for the SSL key |
