# UnityWebGLSpeechDetection
Unity WebGL Package For Speech Detection

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

6 Create a custom MonoBehaviour script to use the `WebGLSpeechDetectionPlugin` API

7 Add a using statement to get access to the `WebGLSpeechDetectionPlugin` namespace

```
using UnityWebGLSpeechDetectionPlugin;
```

## Speech Detection Quick Setup

8 Add a meta reference for `WebGLSpeechDetectionPlugin` to the script

```
        /// <summary>
        /// Reference to the plugin
        /// </summary>
        public WebGLSpeechDetectionPlugin _mWebGLSpeechDetectionPlugin = null;
```

9 In the `start event` check if the plugin is available.

```
        // Use this for initialization
        void Start()
        {
            // indicates the plugin is available
            bool isAvailable = false;

            // check the meta reference to the plugin
            if (_mWebGLSpeechDetectionPlugin)
            {
                // check if the plugin is available
                isAvailable = _mWebGLSpeechDetectionPlugin.IsAvailable();
            }

            // if not available, return
            if (!isAvailable)
            {
                // show a warning
                return;
            }
        }
```

10 In the `start event`, if the plugin is available, subscribe to detection events.

```
        void Start()
        {
            ...

            if (!isAvailable)
            {
                return;
            }

            // subscribe to events
            _mWebGLSpeechDetectionPlugin.OnDetectionResult += HandleDetectionResult;
        }
```

11 Add a handler method to receive speech detection events

```
        /// <summary>
        /// Handler for speech detection events
        /// </summary>
        /// <param name="sender"></param>
        /// <param name="args"></param>
        void HandleDetectionResult(object sender,
            WebGLSpeechDetectionPlugin.SpeechDetectionEventArgs args)
        {
        }
```

## Language Selection Quick Setup

12 Add a field to hold the available languages and dialects

```
        /// <summary>
        /// Reference to the supported languages and dialects
        /// </summary>
        private WebGLSpeechDetectionPlugin.LanguageResult _mLanguageResult = null;
```

13 Use the plugin to get the available languages and dialects

```
        void Start()
        {
            ...

            if (!isAvailable)
            {
                return;
            }

            // Get languages and dialects from plugin
            _mLanguageResult = _mWebGLSpeechDetectionPlugin.GetLanguages();
        }
```

14 Populate the language dropdown using the language result

```
            // prepare the language drop down items
            Utils.PopulateLanguagesDropdown(_mDropDownLanguages, _mLanguageResult);
```

15 Handle language change events from the dropdown

```
            // subscribe to language change events
            if (_mDropDownLanguages)
            {
                _mDropDownLanguages.onValueChanged.AddListener(delegate {
                    Utils.HandleLanguageChanged(_mDropDownLanguages,
                        _mDropDownDialects,
                        _mLanguageResult,
                        _mWebGLSpeechDetectionPlugin);
                });
            }
```

16 Handle dialect change events from the dropdown

```
            // subscribe to dialect change events
            if (_mDropDownDialects)
            {
                _mDropDownDialects.onValueChanged.AddListener(delegate {
                    Utils.HandleDialectChanged(_mDropDownDialects,
                        _mLanguageResult,
                        _mWebGLSpeechDetectionPlugin);
                });
            }
```

17 Before a language is selected, disable the dialect dropdown

```
            // Disabled until a language is selected
            Utils.DisableDialects(_mDropDownDialects);
```

# Fonts

UI text controls need to reference [fonts](https://en.wikipedia.org/wiki/List_of_CJK_fonts) that contain the entire character range for the selected language and dialect in order to display correctly.

[WenQuanYi](https://en.wikipedia.org/wiki/WenQuanYi) is licensed under `GNU General Public License`.
