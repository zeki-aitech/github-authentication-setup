# 🔑 GitHub Authentication with Personal Access Token (PAT)

This guide explains how to authenticate with GitHub over HTTPS using a **Personal Access Token (PAT)** instead of a password — the recommended way since GitHub deprecated password-based authentication.

---

## ✅ When to Use a PAT

- Accessing GitHub over HTTPS (e.g., `https://github.com/username/repo.git`)
- Automating scripts and CI/CD workflows
- When SSH is not available or allowed

---

## 1️⃣ Create a Personal Access Token

1. Go to: [https://github.com/settings/tokens](https://github.com/settings/tokens)
2. Click **"Generate new token"** (→ select "Fine-grained" or "Classic")
3. Set:
   - Token name (e.g., `Git CLI Access`)
   - Expiration (e.g., 90 days)
   - Select scopes:
     - ✅ `repo` (for full repo access)
     - ✅ `workflow` (for GitHub Actions, if needed)
4. Click **"Generate token"**
5. **Copy the token** and store it securely — you won't see it again!

---

## 2️⃣ Use the Token in Git Commands

When Git prompts for your **GitHub password**, use the **token instead**.

### Example:

```bash
git clone https://github.com/yourusername/yourrepo.git
```

When prompted:

```
Username: yourusername
Password: <paste your token here>
```

> 💡 Git will treat the token as your password.

---

## 3️⃣ Cache the Token Securely

To avoid entering the token every time, you can **cache credentials** using Git:

### Temporarily (in memory):
```bash
git config --global credential.helper cache
```

### Permanently (secure system keyring, recommended):
```bash
git config --global credential.helper store
```

> ⚠️ `store` saves your credentials in plaintext (~/.git-credentials) — use with caution.

---

## 4️⃣ Update Remote URL (if needed)

If your remote uses HTTPS and you want to ensure it works with PAT:

```bash
git remote -v
```

To update the remote:
```bash
git remote set-url origin https://github.com/yourusername/yourrepo.git
```

---

## 🛠 Troubleshooting

- **403 errors** → Ensure the token has the right scopes
- **Token not accepted** → Make sure you're using the **token as the password**
- **Token expired** → Revisit GitHub and regenerate a new one

---

## 🔐 Best Practices

- Treat PATs like passwords — never expose them in code
- Use short expiration and regenerate as needed
- Revoke unused or leaked tokens immediately
- Prefer SSH for personal/dev use, PATs for CI

---
