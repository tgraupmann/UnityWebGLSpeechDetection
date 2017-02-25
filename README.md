# UnityWebGLSpeechDetection
The WebGL For Speech Detection package is available in the [Unity Asset Store](https://www.assetstore.unity3d.com/en/#!/content/81076).

# Target

The `Unity WebGL Speech Detection Package` is created for Unity version `5.5` or better.
This package is **only** intended for the `WebGL` platform and requires a browser with the built-in [Web Speech API](https://dvcs.w3.org/hg/speech-api/raw-file/tip/speechapi.html), like Chrome.
Detection requires an Internet connection.
Check the [browser compatibility](https://developer.mozilla.org/en-US/docs/Web/API/Web_Speech_API#Browser_compatibility) to see which browsers implemented the `Speech API`.

# Changelog

1.0 - Initial creation of the project

# Demos

[Demo 01 Unity Speech Dictation](https://theylovegames.com/UnityWebGLSpeechDetection_01Dictation/)

[Demo 02 Unity Speech Commands](https://theylovegames.com/UnityWebGLSpeechDetection_02SpeechCommands/)

# Documentation

This document can be accessed in `Assets/WebGLSpeechDetection/Readme.pdf` or use the menuitem `GameObject->WebGLSpeechDetection->Online Documentation`

# Quick Start

1 Switch to the `WebGL` platform in `Build Settings [image_1](images/image_1.png)

2 Create one `WebGLSpeechDetectionPlugin` GameObject in the scene with the menu `GameObject->WebGLSpeechDetection->Create WebGLSpeechDetectionPlugion` [image_2](images/image_2.png)

3 (Optional) You may need a languages dropdown in your UI, use the menuitem `GameObject->WebGLSpeechDetection->Create Languages Dropdown` [image_3](images/image_3.png)

4 (Optional) You may need a dialects dropdown in your UI, use the menuitem `GameObject->WebGLSpeechDetection->Create Dialects Dropdown` [image_4](images/image_4.png)

5 At this point you should have a scene with the `WebGLSpeechDetectionPlugin`, and (optionally) a couple dropdown controls added to the canvas.

![image_5](images/image_5.png)

6 Create a custom MonoBehaviour script to use the `WebGLSpeechDetection` API

7 Add a using statement to get access to the `WebGLSpeechDetection` namespace

```
using UnityWebGLSpeechDetection;
```

## Speech Detection Quick Setup

8 Add a reference for `WebGLSpeechDetectionPlugin` to the script

```
        /// <summary>
        /// Reference to the plugin
        /// </summary>
        private WebGLSpeechDetectionPlugin _mWebGLSpeechDetectionPlugin = null;
```

9 In the `start event` check if the plugin is available.

```
        // Use this for initialization
        void Start()
        {
            // indicates the plugin is available
            bool isAvailable = false;

            // get the singleton instance
            _mWebGLSpeechDetectionPlugin = WebGLSpeechDetectionPlugin.GetInstance();

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

            // Get languages from plugin,
            _mWebGLSpeechDetectionPlugin.GetLanguages((languageResult) =>
            {
                _mLanguageResult = languageResult;
            });
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

18 Use player prefs to default to the last selected language and dialect

```
                // set the default language
                Utils.SetDefaultLanguage(_mDropDownLanguages);

                // set the default dialect
                Utils.SetDefaultDialect(_mDropDownDialects);
```

# Fonts

UI text controls need to reference [fonts](https://en.wikipedia.org/wiki/List_of_CJK_fonts) that contain the entire character range for the selected language and dialect in order to display correctly.

[WenQuanYi](https://en.wikipedia.org/wiki/WenQuanYi) is licensed under `GNU General Public License`.

# Scenes

## Example01 - Dictation

The scene is located at `Assets/WebGLSpeechDetection/Scenes/Example01_Dictation.unity`

![image_10](images/image_10.png)

## Example02 - Speech Commands

The scene is located at `Assets/WebGLSpeechDetection/Scenes/Example02_SpeechCommands.unity`

![image_11](images/image_11.png)

# Support

Send questions and/or feedback to the support@theylovegames.com email.
