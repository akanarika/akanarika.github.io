---
title: Mini Project 1
date: 2017-02-20 01:16:21
tags: [15664]
---
In the Mini-Project 1, I implemented two of the options, one is CCD IK and the other is Keyframing.

*CCD IK*
platform: Unity 3D
deliverable: CCD/CCD.app
uploaded files: CCD/UnityFiles.tar CCD/CCD.app
description: This app allows us to simulation CCD IK. In this program, we can choose to generate 1 - 90 joints randomly rotated and scaled by using the slider to the top slider. Also, we can choose the iteration counts by changing the value of the slider below. By hitting create button, a set of joints will appear. By holding key "A,S,D,Q,W,E" on the keyboard, you can move the IK handle to the left, down, right, forward, up, backward. By holding key "J,K,L,U,I,O", you can move the camera view in the same way. By hitting one of those joints on the screen, we can set the end effector to any of them. 
process:
![create 5 joints](/images/ccd1.png)
![if the target can't be reached](/images/ccd2.png)
![select the end effector](/images/ccd3.png)
![change the camera view](/images/ccd4.png)

*Keyframing*
platform: Blender
deliverable: Keyframing/squash.blend videos to be uploaded still rendering..
description: This is the first model I've ever done the modeling, texturing, rigging, animating and rendering all by myself. I implemented two walk cycles, one is the normal one, the other angry.
![](/images/render3.png)
![](/images/render4.png)
implementation:
For the rigging part, I followed a standard rigging style for a bipedal character. And then created two knee pole targets, to make sure that the knees of my character are facing forward all the time. Two feet controllers were added to make it convenient to animate the step motion. And I also added two heel IK handlers to make the rotation of the feet more natural.
![rigging](/images/rig.png)
![controllers](/images/handle.png)
Then I followed the [Animators_Survival_Kit](http://graphics.cs.cmu.edu/nsp/course/15464-s17/lectures/Animators_Survival_Kit_walks.pdf) to make the walking cycle, which turned out to be not bad, (satisfied me at least XD ). Then the angry walking cycle, since the motion is a bit exaggerated, end up being a little bumpy. Funny.
{% vimeo 204888847%}
{% vimeo 204913396%}
