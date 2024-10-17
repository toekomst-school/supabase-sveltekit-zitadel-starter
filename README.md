# SvelteKit + Supabase Tutorial

This is the final project of my SvelteKit + Supabase tutorial. It's a super simple app where you can sign in and manage your profile, but it showcases most of the key concepts you need.

**VIDEO LINK: https://youtu.be/lEWghUOta-4**

## Getting Started

1. Clone the repo
2. Install dependencies with `bun i`
3. Create a `.env` based on `.env.example`
4. Start your supabase server with `supabase start`
5. Start your app with `bun run dev`

## Zitadel proxy
To get zitadel working, you need to mod the keycloak extension
based upon the following comment: https://github.com/orgs/supabase/discussions/6547#discussioncomment-9049664

in nginx i added the following config:
```
location /protocol/openid-connect/auth {
    proxy_pass https://zitadel.your-zitadel-domain.com/oauth/v2/authorize;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
}

location /protocol/openid-connect/token {
    proxy_pass https://zitadel.your-zitadel-domain.com/oauth/v2/token;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
}

location /protocol/openid-connect/userinfo {
    proxy_pass https://zitadel.your-zitadel-domain.com/oauth/v2/userinfo;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
}
```
