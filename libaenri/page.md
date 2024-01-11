---
project_name: libaenri
tags:
  - backend
  - rust
  - diesel
  - sql
  - public
  - database
links:
  github: https://github.com/aenriii/libaenri
status: BRAINSTORMING # possible values: ACTIVE, MAINTAINENCE_ONLY, BACKBURNER, INACTIVE, FINISHED, BRAINSTORMING, NULL, ON_HOLD
---

# libaenri

an api wrapping multiple different computations and apis into a few calls of
the same api, with the same api key. Comes complete with email notification 
support and a catppuccin-themed API management panel.

## Features

libaenri will be able to do the following

- Get lyrics to a Spotify song (Unsynced, Synced (line), and Synced (Syllable/Word))
- Get discord user information
  - discord-based user info, such as discord badges, avatar, and profile colors
  - client mod-based user data, such as Decor decorations, 3y3 colors, and badges.
- Get spotify now playing for a given user as a websocket providing updates every x seconds or when a change is made
- Store a discord webhook url and/or an email for if any connected services need reauthentication
- Retrieve Steam status for a user

### Connectable Services

- Discord
- Spotify
- last.fm
- Steam

## Getting Started

> This API is currently being developed, and is not publically available. This is here as fill-in for when I do finish it and make it public.

First, head over to [lib.aenri.loveh.art](https://lib.aenri.loveh.art) and
register using an invite code. Make sure to enable all your preferred security
measures, as I thought it would be pretty cool to support MFA.
> Don't have an invite code? [Sign up for one]() or [Ask a moderator for one]() ([Why do I need an invite code?]()).

Make sure to verify your email and sign in to access your control panel. Here,
you'll be able to connect your services to libaenri and fill in some optional
settings for your account. The following are the settings that are currently
available for use.

### CORS Rules / Domain Blacklist
You can whitelist or blacklist domains for what can and can't use your API key.
This requires either a HEAD request and a client that follows CORS policy or a GET
request and source information

#### Require source information for all requests

If this flag is enabled, any request without a valid `Origin` header will be
immediately denied.

> You can technically use this in your backend with a special cors whitelist to make an extra key you need to provide!

### Alternate last.fm-compatible api

If you'd like to use libre.fm or anything of the sort instead of the official
last.fm, just enter in the api endpoint and save before attacking your
account.

### Steam status options

#### Make VR status visible

Self-explanatory. Enables the `vr` (`boolean`) field in your api response

#### Make Away status visible

Self-explanatory. Enables the `away` (`boolean`) field in your api response

#### Show Rich status where available

Enables the `rich` (`string[]`) field in your api response.

## API Documentation

### Authentication

For authentication, you can either provide an Authorization: Bearer api-key
header or a ?key=api-key URL parameter

### Rate limiting

Each endpoint can draw from either its own counter or from a pool. If you receive
either 50% of your rate limit or 10 requests in 429s, whichever is larger, your
API key will be invalidated and you will have to regenerate an API key. This is
to lessen server load and protect against leaked API keys.

If you have a high-traffic website, you should NOT be pinging an endpoint with 
each request to your server. I run this server as well as about 40 other things
on a poor free-tier Oracle VPS, and would rather not have my vaultwarden
instance throatfucked because you dont know how to set up a cache.

In addition, **if you are consistently hitting your rate limit, your API access**
**will be paused while you set up a cache or make yours better.** If this happens
to you, contact me to re-enable your api access.


### GET `/api/v1/status`

#### Notes for this endpoint
- Authorization not required
- Reguardless of authentication, rate limit is 2requests/60s per IP *endpoint exclusive*

#### Response schema

```json
{
    external_services: {
        steam: boolean,
        spotify: boolean,
        lastfm: boolean,
        discord: boolean
    },
    avgPing: {
        over10m: number,
        over1d: number
    },
    uptime: number,

}
```

### GET `/api/v1/me`

#### Notes for this endpoint
- Authorization is required
- Ratelimit is 20 requests/minute, 100 requests/hour, and 1000 requests/day. 

// todo...