# 使用Github Action + acme.sh 自动申请并续期SSL证书

自动申请SSL 证书,并push到repo

定时检查SSL 证书过期时间，对于小于30天有效期的证书自动续期

同时申请 ECDSA 和 RSA 证书

如有设置，会从主CA和备CA各申请一份ECDSA和一份RSA证书

## 环境变量

### Repository Secrets

1. `ACCOUNT_EMAIL`：用于注册 SSL 证书的电子邮件地址。(必须)
2. `DNSAPI`：DNS API 配置，指定使用的 DNS 提供商进行验证。参见[acme.sh wiki](https://github.com/acmesh-official/acme.sh/wiki/dnsapi),无需"export" (必须)
3. `ZEROSSL_EAB_KEY_ID`：ZeroSSL 的 EAB（External Account Binding）密钥 ID。(当CA=zerossl时必须)
4. `ZEROSSL_EAB_HMAC_KEY`：ZeroSSL 的 EAB HMAC 密钥。(当CA=zerossl时必须)

### Repository Variables

1. `CA`：证书颁发机构(CA) letsencrypt 或 zerossl。(必须)
2. `BACKUP_CA`：备 CA 。(可选)
3. `ECC_KEYLENGTH`：ECC 证书密钥长度， ec-256 或 ec-384。(必须)
4. `RSA_KEYLENGTH`：RSA 证书密钥长度， 2048 或 3072 或 4096。(必须)

## 设置 GitHub Actions 权限

 `Settings -> Code and automation -> Actions -> General -> Workflow permissions -> Read and write permissions ✅`

## 配置域名

修改domains_examples.yaml并重命名为domains.yaml

## 触发

默认 UTC 17:00 即 UTC+8 1:00 执行一次

也可以手动触发

## 已知问题

不知道为什么有时候申请zerossl证书会失败，需要再触发一次action才能申请到

## 致谢

[danbao/auto-ssl](https://github.com/danbao/auto-ssl)

[kimoch111/AutoSSL](https://github.com/kimoch111/AutoSSL)
