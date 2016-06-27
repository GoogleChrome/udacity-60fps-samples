##List of all known bugs:

###CSS issues
* Lots of style recalcs when we bring a story in (`body.details-active .story__title`, etc)
* Double shadow on .header
* Triple(!) shadow on `.story__score` and `.story-details`
* Promoted every single child element in `.story-details`. GO ME [says Paul]. This one will show up when you have visited a few stories. If you check the layers panel you'll see it too.

###onStoryData
* Loops through manually rather than using a `querySelector` to get the right element.
* Makes visual changes outside of a rAF.

###onStoryClick
* Uses a `setTimeout` to start showing the story.
* Just splats the DOM in rather than using a rAF.
* Same for the comments.

###showStory
* Adds an overbroad class on the body.
* Uses `setTimeout` for animation and runs it every 4ms
* Causes forced sync layouts if it runs multiple times per frame due to `getBoundingClientRect` and `storyDetails` `left` style setting.

###hideStory
* Same as above.

###colorizeAndScaleStories
* Completely unnecessary effect (interesting to see if any students drop it altogether - you should consider it IMO, but if not there's loads they can do).
* Colors every single score.
* Sets the width and height (should be a scale transform) triggering a global layout.
* Then reads it back to figure the color it needs (way daft).
* Triggers layout thrashing in the process.

###touchstart
* This just shouldn't be here and it just periodically kills touch input, so hopefully you'll realize what a bad thing touch handlers can be.

###scroll
* Really, we don't want to color and scale the scores.
* Should be in a `requestAnimationFrame` as it makes visual changes.

###loadStoryBatch
* Making visual changes outside of a requestAnimationFrame.

###App.Data.get*
* Could be done in a worker (although likely not a big deal)

###Bonuses
* Inline scripts in the top of the head.
* Fixed position header will be repainting (`.header`) on low DPI devices.
* So will `.main` (low DPI only) so ideally it needs promoting.
