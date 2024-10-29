以下是一个详细的 `README` 文档，可以帮助用户了解如何使用该程序：

---

# JWT Brute Force Tool

此项目是一个用于生成、破解和暴力破解 JSON Web Token (JWT) 的工具。该工具支持多线程优化，可以使用字典文件进行破解或使用暴力破解模式尝试所有可能的字符组合。

## 功能概述

该工具支持以下四种操作模式：

1. `gen`：生成未加密的 JWT。
2. `genWithSecret`：使用指定密钥生成 JWT。
3. `crack`：使用字典文件尝试破解 JWT 密钥。
4. `brute`：使用暴力破解模式，尝试所有字符组合来破解 JWT 密钥。

## 安装

确保已安装 [Go 编译器](https://golang.org/doc/install)。

1. 克隆此仓库：

   ```bash
   git clone <repository-url>
   cd <repository-directory>
   ```

2. 编译源代码：

   ```bash
   go build -o jwt_tool main.go
   ```

3. 使用帮助命令查看支持的功能：

   ```bash
   ./jwt_tool --help
   ```

## 使用说明

以下是各命令的详细使用说明：

### 1. `gen` - 生成未加密的 JWT

生成未加密的 JWT（使用 `none` 签名算法）。

```bash
./jwt_tool gen -payload <JSON字符串>
```

示例：

```bash
./jwt_tool gen -payload '{"user":"testuser","admin":false}'
```

### 2. `genWithSecret` - 使用密钥生成 JWT

生成带有指定密钥的 JWT（使用 `HS256` 签名算法）。

```bash
./jwt_tool genWithSecret -payload <JSON字符串> -secret <密钥>
```

示例：

```bash
./jwt_tool genWithSecret -payload '{"user":"testuser","admin":false}' -secret "mysecret"
```

### 3. `crack` - 使用字典文件破解 JWT

使用字典文件中的密钥尝试破解 JWT。

```bash
./jwt_tool crack -token <JWT字符串> -dict <字典文件路径>
```

示例：

```bash
./jwt_tool crack -token "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjoidGVzdHVzZXIiLCJhZG1pbiI6ZmFsc2V9.X7dG3m4U2u3wEZuRmfs8HY_LhCw1JlCye0uPfyfXhmg" -dict passwords.txt
```

### 4. `brute` - 使用暴力破解破解 JWT

使用暴力破解模式尝试所有字符组合来破解 JWT 密钥。

```bash
./jwt_tool brute -token <JWT字符串> -minLen <最小长度> -maxLen <最大长度> -charset <字符集> -threads <线程数>
```

参数说明：

- `minLen`：最小密钥长度。
- `maxLen`：最大密钥长度。
- `charset`：暴力破解使用的字符集，默认字符集为 `abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789`。
- `threads`：线程数，`0` 表示使用系统的所有核心线程。

示例：

```bash
./jwt_tool brute -token "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjoidGVzdHVzZXIiLCJhZG1pbiI6ZmFsc2V9.X7dG3m4U2u3wEZuRmfs8HY_LhCw1JlCye0uPfyfXhmg" -minLen 1 -maxLen 4 -charset "abc" -threads 4
```

### 示例解释

- 使用字典破解时，会遍历字典文件中的每一行，尝试使用每个密钥解密 JWT，直到找到正确的密钥。
- 暴力破解模式会尝试使用指定长度和字符集的所有可能组合。如果设置了 `threads` 为 `0`，则会自动使用所有可用 CPU 核心来加速破解。

## 错误处理

- 确保 `-payload` 参数中的 JSON 格式有效，以避免生成 JWT 失败。
- 使用 `crack` 模式时，确保字典文件存在且格式正确。

## 注意事项

使用此工具时需遵守相关法律和合规要求，未经授权的情况下破解或生成他人的 JWT 是违法的。该工具仅供安全研究和教育用途。
