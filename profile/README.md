<p align="center"><img src="https://raw.githubusercontent.com/go-instagram/brand/main/social/go-instagram.png" alt="go-instagram" width="640"></p>

<h1 align="center">go-instagram</h1>
<p align="center">Pure-Go best-effort read client for public Instagram content.</p>
<p align="center"><a href="https://go-instagram.github.io/docs/"><img src="https://img.shields.io/badge/docs-mkdocs--material-0A6E96?style=flat-square&logo=materialformkdocs&logoColor=white" alt="docs"></a> <a href="https://pkg.go.dev/github.com/go-instagram/instagram"><img src="https://img.shields.io/badge/pkg.go.dev-reference-0079A8?style=flat-square&logo=go&logoColor=white" alt="pkg.go.dev"></a> <img src="https://img.shields.io/badge/Go-1.26-00ADD8?style=flat-square&logo=go&logoColor=white" alt="Go"> <img src="https://img.shields.io/badge/license-BSD--3--Clause-0A6E96?style=flat-square" alt="license"></p>

---

## What is this?

A pure-Go, dependency-free, **best-effort** read client for public Instagram content served through Instagram's web JSON endpoints. The Go API is kept deliberately small and stable so your code can survive the churn underneath — the underlying transport may break at any time regardless.

The client lives in [`go-instagram/instagram`](https://github.com/go-instagram/instagram):

```go
// A sessionid cookie is usually required for reads to succeed.
c := instagram.New(instagram.WithSessionID("your-sessionid-cookie"))

prof, err := c.UserProfile(context.Background(), "instagram")
if err != nil {
	panic(err) // 401/403/429 here means Instagram is blocking the request.
}
fmt.Printf("%s (%s) — %d followers\n", prof.FullName, prof.Username, prof.Followers)
for _, p := range prof.Posts {
	fmt.Printf("- %s  %d likes  %s\n", p.Permalink, p.Likes, p.Caption)
}
```

## Install

```sh
go get github.com/go-instagram/instagram
```

## ⚠️ Best-effort — read this first

Instagram does not offer these endpoints as a stable, documented public API. They are the internal endpoints its own website calls, and they change, rate-limit, and lock without notice.

Unauthenticated requests are frequently rejected — you will often need a valid logged-in `sessionid` cookie for reads to succeed. Any request can start returning 401 / 403 / 429 at any time when Instagram decides to block you.

## Links

- 📖 Docs — <https://go-instagram.github.io/docs/>
- 🌐 Site — <https://go-instagram.github.io/>
- 🧩 Client — <https://github.com/go-instagram/instagram>
- 📦 API reference — <https://pkg.go.dev/github.com/go-instagram/instagram>
- 🎨 Brand assets — <https://github.com/go-instagram/brand>

---
<p align="center"><sub>Branding in <a href="https://github.com/go-instagram/brand">go-instagram/brand</a>.</sub></p>
