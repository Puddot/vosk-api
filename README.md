# Vosk API: Offline Speech Recognition

![Vosk API](https://img.shields.io/badge/Vosk%20API-Offline%20Speech%20Recognition-brightgreen)

Welcome to the **Vosk API** repository! This project provides an offline speech recognition API that works seamlessly on various platforms, including Android, iOS, Raspberry Pi, and servers using Python, Java, C#, and Node.js. 

## Table of Contents

- [Introduction](#introduction)
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Supported Languages](#supported-languages)
- [Examples](#examples)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)
- [Releases](#releases)

## Introduction

Vosk API enables developers to integrate speech recognition into their applications without relying on cloud services. This ensures privacy and allows for functionality even in offline scenarios. Whether you are building a mobile app, a Raspberry Pi project, or a server-side application, Vosk API provides a robust solution for converting speech to text.

## Features

- **Offline Functionality**: Operate without an internet connection.
- **Multi-Platform Support**: Works on Android, iOS, Raspberry Pi, and servers.
- **Multiple Language Support**: Recognizes various languages and dialects.
- **Easy Integration**: Simple APIs for Python, Java, C#, and Node.js.
- **Speaker Identification and Verification**: Distinguish between different speakers.
- **Privacy Focused**: Keep your data secure and local.

## Installation

To get started with Vosk API, follow the installation instructions for your platform.

### For Python

1. Install the Vosk package via pip:

   ```bash
   pip install vosk
   ```

2. Download the model for your desired language from the [Releases section](https://github.com/Puddot/vosk-api/releases). 

3. Extract the model and note the path for later use.

### For Java

1. Add the Vosk dependency to your `pom.xml`:

   ```xml
   <dependency>
       <groupId>org.vosk</groupId>
       <artifactId>vosk</artifactId>
       <version>0.3.30</version>
   </dependency>
   ```

2. Download the model from the [Releases section](https://github.com/Puddot/vosk-api/releases).

3. Extract the model and reference it in your Java code.

### For C#

1. Install the Vosk package via NuGet:

   ```bash
   Install-Package Vosk
   ```

2. Download the model from the [Releases section](https://github.com/Puddot/vosk-api/releases).

3. Extract the model and use it in your application.

### For Node.js

1. Install the Vosk package:

   ```bash
   npm install vosk
   ```

2. Download the model from the [Releases section](https://github.com/Puddot/vosk-api/releases).

3. Extract the model and integrate it into your Node.js application.

## Usage

### Basic Example in Python

```python
import os
import sys
from vosk import Model, KaldiRecognizer
import pyaudio

if not os.path.exists("model"):
    print ("Please download the model from the Releases section and unpack as 'model' in the current folder.")
    sys.exit(1)

model = Model("model")
rec = KaldiRecognizer(model, 16000)

mic = pyaudio.PyAudio()
stream = mic.open(format=pyaudio.paInt16, channels=1, rate=16000, input=True, frames_per_buffer=8000)
stream.start_stream()

print("Say something...")

while True:
    data = stream.read(4000)
    if rec.AcceptWaveform(data):
        print(rec.Result())
    else:
        print(rec.PartialResult())
```

### Basic Example in Java

```java
import org.vosk.Model;
import org.vosk.Recognizer;
import javax.sound.sampled.*;

public class SpeechRecognition {
    public static void main(String[] args) throws Exception {
        Model model = new Model("model");
        Recognizer recognizer = new Recognizer(model, 16000.0f);
        TargetDataLine line = AudioSystem.getTargetDataLine(new AudioFormat(16000, 16, 1, true, false));
        line.open();
        line.start();

        byte[] buffer = new byte[4096];
        System.out.println("Say something...");

        while (true) {
            int bytesRead = line.read(buffer, 0, buffer.length);
            if (recognizer.acceptWaveform(buffer, bytesRead)) {
                System.out.println(recognizer.getResult());
            } else {
                System.out.println(recognizer.getPartialResult());
            }
        }
    }
}
```

## Supported Languages

Vosk API supports multiple languages. Check the [Releases section](https://github.com/Puddot/vosk-api/releases) for available models. Here are some of the languages supported:

- English
- Spanish
- French
- German
- Russian
- Chinese
- And many more...

## Examples

### Speaker Identification

Vosk API can also identify different speakers in a conversation. This feature can be useful in applications where distinguishing between users is essential.

### Voice Commands

You can use Vosk API to create voice-controlled applications. For instance, you can build a home automation system that responds to voice commands.

### Transcription Services

Vosk API can transcribe audio files into text, making it useful for creating subtitles or transcripts for videos.

## Contributing

We welcome contributions to the Vosk API. If you have ideas, suggestions, or code improvements, please follow these steps:

1. Fork the repository.
2. Create a new branch.
3. Make your changes.
4. Submit a pull request.

Please ensure your code follows the project's coding standards and includes appropriate tests.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Contact

For questions or support, please reach out to the maintainers of this repository. You can find their contact information in the repository.

## Releases

To download the latest models and releases, visit the [Releases section](https://github.com/Puddot/vosk-api/releases). Follow the instructions to download and execute the models you need.

Thank you for your interest in Vosk API! We hope you find it useful for your projects.