---
project_name: beautiful-lyrics-svelte
tags:
  - web
  - typescript
  - svelte
links:
  github: https://github.com/aenriii/beautiful-lyrics-svelte
status: BACKBURNER # possible values: ACTIVE, MAINTAINENCE_ONLY, BACKBURNER, INACTIVE, FINISHED, BRAINSTORMING, NULL, ON_HOLD
---

# beautiful-lyrics-svelte

A Svelte component meant to mimic the behavior of the Beautiful Lyrics plugin
for Spicetify.

## Examples

> Disclaimer: This is a mockup made in figma, and does not display the actual development progress.

<center> <img src="./beautiful-lyrics-svelte-example-1.png" /> </center>

## Usage

> Hint: This is intended for use with [libaenri](). You'll need to make your
own now playing provider with a compatible signature for this to work.

```tsx

<script>
    import { type NowPlayingProvider } from '@aenriii/common-types';
    import { BeautifulLyrics } from '@aenriii/beautiful-lyrics-svelte';
    // Hint: this is provided if you use libaenri-ts!
    export let provider: NowPlayingProvider
</script>

<BeautifulLyrics 
    provider=provider,
    class="beautifyl-lyrics"
/>


```