# Hello, TJBot!

> :robot: :speaker: Say hello, TJBot!

This recipe provides a simple example for how to make TJBot say hello using Text to Speech (TTS).

## Requirements

![Raspberry Pi 4](https://img.shields.io/badge/Raspberry%20Pi-4+-red)
![Speaker](https://img.shields.io/badge/Hardware-Speaker-brightgreen)
![Node.js](https://img.shields.io/badge/Node.js-20%2B-green)

> ⚠️ We recommend a Raspberry Pi 4+ for local TTS synthesis. The receipe will work on other Raspberry Pi hardware using one of the cloud-based TTS backends.

## How It Works

This recipe demonstrates TJBot's speech capabilities by having it say hello using text-to-speech synthesis. By default, text-to-speech synthesis runs **locally on the Raspberry Pi** using [Sherpa-ONNX](https://github.com/k2-fsa/sherpa-onnx), a lightweight on-device speech recognition engine that requires no internet connection or cloud API keys.

This recipe can be also configured to use cloud-based text-to-speech providers:

- [IBM Watson Speech to Text](https://www.ibm.com/products/speech-to-text)
- [Google Cloud Speech-to-Text](https://cloud.google.com/speech-to-text)
- [Microsoft Azure Speech](https://azure.microsoft.com/en-us/products/cognitive-services/speech-services)

## Configure

> 🔧 Prerequisite: Make sure you have configured your Raspberry Pi for TJBot by following the [bootstrap instructions](https://github.com/tjbot-ce/tjbot/wiki/Bootstrapping-TJBot).

### Install dependencies

Open a Terminal, navigate to the `tjbot/recipes/hello_tjbot` directory, and install the dependencies.

```sh
cd tjbot/recipes/hello_tjbot
npm install
```

## Run

Run this recipe using the following command.

```sh
npm start
```

You should see the following output:

```sh
$ npm start

> hello_tjbot@3.0.0 start
> node index.js

info: 👋 Hello from TJBot! Running on Raspberry Pi 5 Model B Rev 1.0
info: 🤖 Initializing TJBot with speaker
info: 💬 TJBot speaking: "Hello! My name is TJBot and it is very nice to meet you!"
info: 📦 Downloading sherpa-onnx model: Ryan (US male, medium quality, ~50MB)
info: Downloading from https://github.com/k2-fsa/sherpa-onnx/releases/download/tts-models/vits-piper-en_US-ryan-medium.tar.bz2
Downloading [████████████████████████████████████████] 100% | 64/64 MB
info: Download complete
info: 📦 Extracting model...
info: 📦 Successfully downloaded sherpa-onnx model: Ryan (US male, medium quality, ~50MB) (en_US-ryan-medium.onnx)
info: 🗣️ Sherpa-ONNX TTS engine initialized
info: 💬 Loading TTS model: vits-piper-en_US-ryan-medium
info: 💬 TTS model loaded successfully
```

> ⚠️ The first time you run this script, your TJBot will download a Speech to Text model. This download may take a little time, please be patient!

## Customize

### Customization 1: Change the greeting

You can change how TJBot greets you by editing `index.js` and modifying the text on this line:

```js
/* Customization 1: Change the greeting message */
tj.speak('Hello! My name is TJBot and it is very nice to meet you!');
```

### Customization 2: Change the voice

Have TJBot speak in a different voice by editing `tjbot.toml`. First, comment out the lines for the Ryan voice by adding a '#' character in front of them:

```toml
# Ryan (en_US, male)
#model = 'vits-piper-en_US-ryan-medium'
#modelUrl = 'https://github.com/k2-fsa/sherpa-onnx/releases/download/tts-models/vits-piper-en_US-ryan-medium.tar.bz2'
```

Next, uncomment the lines for the Kathleen voice by removing the '#' character in front of them:

```toml
# Kathleen (en_US, female)
model = 'vits-piper-en_US-kathleen-low'
modelUrl = 'https://github.com/k2-fsa/sherpa-onnx/releases/download/tts-models/vits-piper-en_US-kathleen-low.tar.bz2'
```

### Customization 3: Use a Cloud-baed TTS service

You can switch the text-to-speech backend used to synthesize TJBot's voice by editing `tjbot.toml` and changing the backend to one of these options:

```toml
# Customization 3: Try one of these cloud-based TTS services.
# Be sure to include your credentials in the appropriate file.
#type = 'ibm-watson-tts'    # store credentials in ibm-credentials.env
#type = 'google-cloud-tts'  # store credentials in google-credentials.json
#type = 'azure-tts'         # store credentials in azure-credentials.env
```

> ⚠️ Be sure to comment out `type = 'local'` to ensure TJBot uses one of the cloud-based TTS backends.

Next, you will need to create an instance of the text to speech service on your cloud provider and download the file containing your API credentials. Place that file either in `tjbot/recipes/hello_tjbot` or `~/.tjbot`.

## Troubleshoot

If you are having difficulties in making this recipe work, please see the [troubleshooting guide](https://github.com/tjbot-ce/tjbot/wiki/Troubleshooting-TJBot).

## Contribute

If you would like to contribute to TJBot, please see the [contributor's guide](https://github.com/tjbot-ce/tjbot/wiki/Contributing-to-TJBot).

## License

This project is licensed under Apache 2.0. Full license text is available in [LICENSE](../../LICENSE).
