# Plyr
A simple, accessible and customizable HTML5, YouTube and Vimeo media player.

[Checkout the demo](https://plyr.io)

[Read the original repo readme](https://github.com/Selz/plyr/readme.md)

## What's in the fork?

new player type - `audioslides` which allows html5 audio to be synced with a slideshow inside the plyr instance. Why? Because plyr looks neat, means you don't have to muck about with a custom full screen implementation, and plyr already has almost all the required caption handling.

Lets say you have this setup for your instance data source:

     s.source({
        type: "audioslides",
        title: "slides in iframe demo",
        sources: [{
                src: "content/some-presentation.mp3",
                type: "audio/mp3"
            }, {
                src: "content/some-presentation.ogg",
                type: "audio/ogg"
            }],
         poster: "content/poster.png",
          tracks: [{
              kind: "chapters",
              label: "English",
              srclang: "en",
              src: "content/slides.vtt",
              "default": !0
          }]
       });

Yep, that's a `poster` on an `audio` player. It's actually just an `img` tag inside the element, if present. It appears before playback begins, just like on a `video` tag.

Your content/slides.vtt file might look like this. The `id`, which is the first line before a time marker, is the source path for your slide. It's up to you to ensure that its content fits and scales how you want.

        WEBVTT FILE

        slides-1.html
        00:00:00.001 --> 00:00:06.000

        slides-2.html
        00:00:06.001 --> 00:00:12.500

        slides-3.html
        00:00:12.500 --> 00:00:28.000

        slides-4.html
        00:00:32.500 --> 00:00:34.500
        hello

If you add a text node to the marker, it will appear as a caption. That's not how the spec really works, but it's how this fork works for now.

If you leave "gaps" in the chapter markers (time values where no marker exist) then if you manually seek then it won't find those queues until the next cue change.

