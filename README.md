# UnityWebGLSpeechDetection
Unity WebGL Module For Speech Detection

# Target

The `Unity WebGL Speech Detection Package` is **only** intended for the `WebGL` platform and requires the `Chrome` browser.
Speech detection uses the browser's built-in [Web Speech API](https://dvcs.w3.org/hg/speech-api/raw-file/tip/speechapi.html) and requires an Internet connection.
Check the [browser compatibility](https://developer.mozilla.org/en-US/docs/Web/API/Web_Speech_API#Browser_compatibility) roadmap for browsers with the `Speech API` feature in development.

# Changelog

1.0 - Initial creation of the project

# Demos

[Demo 01 Unity Speech Dictation](https://theylovegames.com/UnityWebGLSpeechDetection_01Dictation/)

[Demo 02 Unity Speech Commands](https://theylovegames.com/UnityWebGLSpeechDetection_02SpeechCommands/)

# Documentation

This document can be accessed in `Assets/WebGLSpeechDetection/Readme.pdf` or use the menuitem `GameObject->WebGLSpeechDetection->Online Documentation`

# Quick Start

1 Switch to the `WebGL` platform in `Build Settings [?](images/image_1.png)

2 Create one `WebGLSpeechDetectionPlugin` GameObject in the scene with the menu `GameObject->WebGLSpeechDetection->Create WebGLSpeechDetectionPlugion` [?](images/image_2.png)

3 (Optional) You may need a languages dropdown in your UI, use the menuitem `GameObject->WebGLSpeechDetection->Create Languages Dropdown` [?](images/image_3.png)

4 (Optional) You may need a dialects dropdown in your UI, use the menuitem `GameObject->WebGLSpeechDetection->Create Dialects Dropdown` [?](images/image_4.png)

5 At this point you should have a scene with the `WebGLSpeechDetectionPlugin`, and (optionally) a couple dropdown controls added to the canvas.

![image_5](images/image_5.png)

# Fonts

UI text controls need to reference [fonts](https://en.wikipedia.org/wiki/List_of_CJK_fonts) that contain the entire character range for the selected language and dialect in order to display correctly.

[WenQuanYi](https://en.wikipedia.org/wiki/WenQuanYi) is licensed under `GNU General Public License`.
