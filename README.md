# assets_example

## Adding assets and images

Here’s a summary of the [Flutter documentation on **Assets and Images**](https://docs.flutter.dev/ui/assets/assets-and-images), using the same method with explanations and **code examples**:

---

### **Flutter Assets and Images**
Flutter allows you to bundle assets (like images, fonts, and data files) with your app. These assets can be accessed at runtime to display images, load fonts, or read data.

---

### **1. Adding Assets**
To include assets in your app, you need to declare them in the `pubspec.yaml` file.

#### Example:
```yaml
flutter:
  assets:
    - assets/images/logo.png
    - assets/data/config.json
```

---

### **2. Loading Images**
You can load images using the `AssetImage` or `Image.asset` widget.

#### Example:
```dart
Image.asset('assets/images/logo.png');
```

---

### **3. Loading Images with Different Resolutions**
Flutter supports resolution-aware images by naming files with suffixes like `1.5x`, `2.0x`, etc.

#### Example:
```yaml
flutter:
  assets:
    - assets/images/logo.png
    - assets/images/logo_1.5x.png
    - assets/images/logo_2.0x.png
```

```dart
Image.asset('assets/images/logo.png');
```

---

### **4. Loading Fonts**
You can load custom fonts by declaring them in the `pubspec.yaml` file.

#### Example:
```yaml
flutter:
  fonts:
    - family: MyCustomFont
      fonts:
        - asset: assets/fonts/MyCustomFont-Regular.ttf
        - asset: assets/fonts/MyCustomFont-Bold.ttf
          weight: 700
```

```dart
Text(
  'Hello, Flutter!',
  style: TextStyle(fontFamily: 'MyCustomFont', fontWeight: FontWeight.bold),
);
```

---

### **5. Loading Data Files**
You can load data files (e.g., JSON) using the `rootBundle` or `DefaultAssetBundle`.

#### Example:
```dart
import 'package:flutter/services.dart';

Future<String> loadAsset() async {
  return await rootBundle.loadString('assets/data/config.json');
}
```

---

### **6. Using `AssetImage`**
The `AssetImage` class is used to load images from the asset bundle.

#### Example:
```dart
DecorationImage(
  image: AssetImage('assets/images/background.png'),
);
```

---

### **7. Combining Properties**
Here’s an example combining multiple properties:

#### Example:
```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('Assets and Images')),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              Image.asset('assets/images/logo.png'),
              Text(
                'Hello, Flutter!',
                style: TextStyle(fontFamily: 'MyCustomFont', fontSize: 24),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

---

### **Summary of Assets and Images**
| Property              | Description                              | Example                                   |
|-----------------------|------------------------------------------|-------------------------------------------|
| `assets` in `pubspec.yaml` | Declares assets in the app          | `assets: ['assets/images/logo.png']`      |
| `Image.asset`         | Loads an image from assets               | `Image.asset('assets/images/logo.png')`   |
| `AssetImage`          | Loads an image for use in widgets        | `AssetImage('assets/images/logo.png')`    |
| `fonts` in `pubspec.yaml` | Declares custom fonts               | `fonts: [{family: 'MyCustomFont', ...}]`  |
| `rootBundle`          | Loads data files from assets             | `rootBundle.loadString('assets/data/config.json')` |

---

### **Example: Full Usage**
Here’s a complete example of using assets and images in a Flutter app:
```dart
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('Assets and Images')),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              Image.asset('assets/images/logo.png'),
              Text(
                'Hello, Flutter!',
                style: TextStyle(fontFamily: 'MyCustomFont', fontSize: 24),
              ),
              FutureBuilder(
                future: loadAsset(),
                builder: (context, snapshot) {
                  if (snapshot.connectionState == ConnectionState.done) {
                    return Text('Data: ${snapshot.data}');
                  }
                  return CircularProgressIndicator();
                },
              ),
            ],
          ),
        ),
      ),
    );
  }

  Future<String> loadAsset() async {
    return await rootBundle.loadString('assets/data/config.json');
  }
}
```

---

## Custom Font 

Here’s a summary of the [Flutter documentation on **Using Custom Fonts**](https://docs.flutter.dev/cookbook/design/fonts), using the same method with explanations and **code examples**:

---

### **Flutter Custom Fonts**
Flutter allows you to use custom fonts in your app by bundling font files (e.g., `.ttf` or `.otf`) and declaring them in the `pubspec.yaml` file.

---

### **1. Adding Fonts**
To use custom fonts, you need to:
1. Add the font files to your project (e.g., in the `assets/fonts` folder).
2. Declare the fonts in the `pubspec.yaml` file.

#### Example:
```yaml
flutter:
  fonts:
    - family: MyCustomFont
      fonts:
        - asset: assets/fonts/MyCustomFont-Regular.ttf
        - asset: assets/fonts/MyCustomFont-Bold.ttf
          weight: 700
```

---

### **2. Using Custom Fonts**
Once declared, you can use the custom font in your app by specifying the `fontFamily` in the `TextStyle`.

#### Example:
```dart
Text(
  'Hello, Flutter!',
  style: TextStyle(
    fontFamily: 'MyCustomFont',
    fontSize: 24,
    fontWeight: FontWeight.bold,
  ),
);
```

---

### **3. Using Multiple Font Weights**
If your font family includes multiple weights (e.g., regular, bold), you can specify the `fontWeight` to use the appropriate variant.

#### Example:
```daml
flutter:
  fonts:
    - family: MyCustomFont
      fonts:
        - asset: assets/fonts/MyCustomFont-Regular.ttf
          weight: 400
        - asset: assets/fonts/MyCustomFont-Bold.ttf
          weight: 700
```

```dart
Text(
  'Hello, Flutter!',
  style: TextStyle(
    fontFamily: 'MyCustomFont',
    fontSize: 24,
    fontWeight: FontWeight.bold, // Uses the bold variant
  ),
);
```

---

### **4. Using Custom Fonts in a Theme**
You can apply custom fonts globally by defining them in the app's theme.

#### Example:
```dart
MaterialApp(
  theme: ThemeData(
    textTheme: TextTheme(
      headline1: TextStyle(
        fontFamily: 'MyCustomFont',
        fontSize: 32,
        fontWeight: FontWeight.bold,
      ),
      bodyText1: TextStyle(
        fontFamily: 'MyCustomFont',
        fontSize: 16,
        fontWeight: FontWeight.normal,
      ),
    ),
  ),
  home: MyHomePage(),
);
```

---

### **5. Combining Properties**
Here’s an example combining multiple properties:

#### Example:
```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      theme: ThemeData(
        textTheme: TextTheme(
          headline1: TextStyle(
            fontFamily: 'MyCustomFont',
            fontSize: 32,
            fontWeight: FontWeight.bold,
          ),
          bodyText1: TextStyle(
            fontFamily: 'MyCustomFont',
            fontSize: 16,
            fontWeight: FontWeight.normal,
          ),
        ),
      ),
      home: Scaffold(
        appBar: AppBar(title: Text('Custom Fonts')),
        body: Center(
          child: Text(
            'Hello, Flutter!',
            style: Theme.of(context).textTheme.headline1,
          ),
        ),
      ),
    );
  }
}
```

---

### **Summary of Custom Fonts**
| Property              | Description                              | Example                                   |
|-----------------------|------------------------------------------|-------------------------------------------|
| `fonts` in `pubspec.yaml` | Declares custom fonts               | `fonts: [{family: 'MyCustomFont', ...}]`  |
| `fontFamily`          | Specifies the custom font family         | `fontFamily: 'MyCustomFont'`              |
| `fontWeight`          | Specifies the font weight                | `fontWeight: FontWeight.bold`             |
| `TextTheme`           | Applies fonts globally in the theme      | `textTheme: TextTheme(...)`               |

---

### **Example: Full Usage**
Here’s a complete example of using custom fonts in a Flutter app:
```dart
import 'package:flutter/material.dart';

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      theme: ThemeData(
        textTheme: TextTheme(
          headline1: TextStyle(
            fontFamily: 'MyCustomFont',
            fontSize: 32,
            fontWeight: FontWeight.bold,
          ),
          bodyText1: TextStyle(
            fontFamily: 'MyCustomFont',
            fontSize: 16,
            fontWeight: FontWeight.normal,
          ),
        ),
      ),
      home: Scaffold(
        appBar: AppBar(title: Text('Custom Fonts')),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              Text(
                'Hello, Flutter!',
                style: Theme.of(context).textTheme.headline1,
              ),
              Text(
                'This is a custom font.',
                style: Theme.of(context).textTheme.bodyText1,
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

---

## Assets and images

Here’s a summary of the [Flutter documentation on **Assets and Images**](https://docs.flutter.dev/ui/assets/assets-and-images), using the same method with explanations and **code examples**:

---

### **Flutter Assets and Images**
Flutter allows you to bundle assets (like images, fonts, and data files) with your app. These assets can be accessed at runtime to display images, load fonts, or read data.

---

### **1. Adding Assets**
To include assets in your app, you need to declare them in the `pubspec.yaml` file.

#### Example:
```yaml
flutter:
  assets:
    - assets/images/logo.png
    - assets/data/config.json
```

---

### **2. Loading Images**
You can load images using the `AssetImage` or `Image.asset` widget.

#### Example:
```dart
Image.asset('assets/images/logo.png');
```

---

### **3. Loading Images with Different Resolutions**
Flutter supports resolution-aware images by naming files with suffixes like `1.5x`, `2.0x`, etc.

#### Example:
```yaml
flutter:
  assets:
    - assets/images/logo.png
    - assets/images/logo_1.5x.png
    - assets/images/logo_2.0x.png
```

```dart
Image.asset('assets/images/logo.png');
```

---

### **4. Loading Fonts**
You can load custom fonts by declaring them in the `pubspec.yaml` file.

#### Example:
```yaml
flutter:
  fonts:
    - family: MyCustomFont
      fonts:
        - asset: assets/fonts/MyCustomFont-Regular.ttf
        - asset: assets/fonts/MyCustomFont-Bold.ttf
          weight: 700
```

```dart
Text(
  'Hello, Flutter!',
  style: TextStyle(fontFamily: 'MyCustomFont', fontWeight: FontWeight.bold),
);
```

---

### **5. Loading Data Files**
You can load data files (e.g., JSON) using the `rootBundle` or `DefaultAssetBundle`.

#### Example:
```dart
import 'package:flutter/services.dart';

Future<String> loadAsset() async {
  return await rootBundle.loadString('assets/data/config.json');
}
```

---

### **6. Using `AssetImage`**
The `AssetImage` class is used to load images from the asset bundle.

#### Example:
```dart
DecorationImage(
  image: AssetImage('assets/images/background.png'),
);
```

---

### **7. Combining Properties**
Here’s an example combining multiple properties:

#### Example:
```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('Assets and Images')),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              Image.asset('assets/images/logo.png'),
              Text(
                'Hello, Flutter!',
                style: TextStyle(fontFamily: 'MyCustomFont', fontSize: 24),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

---

### **Summary of Assets and Images**
| Property              | Description                              | Example                                   |
|-----------------------|------------------------------------------|-------------------------------------------|
| `assets` in `pubspec.yaml` | Declares assets in the app          | `assets: ['assets/images/logo.png']`      |
| `Image.asset`         | Loads an image from assets               | `Image.asset('assets/images/logo.png')`   |
| `AssetImage`          | Loads an image for use in widgets        | `AssetImage('assets/images/logo.png')`    |
| `fonts` in `pubspec.yaml` | Declares custom fonts               | `fonts: [{family: 'MyCustomFont', ...}]`  |
| `rootBundle`          | Loads data files from assets             | `rootBundle.loadString('assets/data/config.json')` |

---

### **Example: Full Usage**
Here’s a complete example of using assets and images in a Flutter app:
```dart
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('Assets and Images')),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              Image.asset('assets/images/logo.png'),
              Text(
                'Hello, Flutter!',
                style: TextStyle(fontFamily: 'MyCustomFont', fontSize: 24),
              ),
              FutureBuilder(
                future: loadAsset(),
                builder: (context, snapshot) {
                  if (snapshot.connectionState == ConnectionState.done) {
                    return Text('Data: ${snapshot.data}');
                  }
                  return CircularProgressIndicator();
                },
              ),
            ],
          ),
        ),
      ),
    );
  }

  Future<String> loadAsset() async {
    return await rootBundle.loadString('assets/data/config.json');
  }
}
```

---

## Reading File System 

Here’s a summary of the [Flutter `File` class documentation](https://api.flutter.dev/flutter/dart-io/File-class.html), using the same method with explanations and **code examples**:

---

### **Flutter `File` Class**
The `File` class in the `dart:io` library provides methods for reading, writing, and manipulating files on the file system. It is commonly used for file I/O operations in Flutter apps.

---

### **1. Basic Usage**
To use the `File` class, you need to import the `dart:io` library.

#### Example:
```dart
import 'dart:io';

void main() {
  File file = File('example.txt');
  file.writeAsStringSync('Hello, Flutter!');
  print(file.readAsStringSync());
}
```

---

### **2. Reading a File**
You can read the contents of a file using the `readAsString` or `readAsStringSync` methods.

#### Example:
```dart
import 'dart:io';

void main() {
  File file = File('example.txt');
  String contents = file.readAsStringSync();
  print(contents);
}
```

---

### **3. Writing to a File**
You can write to a file using the `writeAsString` or `writeAsStringSync` methods.

#### Example:
```dart
import 'dart:io';

void main() {
  File file = File('example.txt');
  file.writeAsStringSync('Hello, Flutter!');
}
```

---

### **4. Appending to a File**
You can append to a file using the `writeAsString` or `writeAsStringSync` methods with the `mode` parameter set to `FileMode.append`.

#### Example:
```dart
import 'dart:io';

void main() {
  File file = File('example.txt');
  file.writeAsStringSync('\nAppended text', mode: FileMode.append);
}
```

---

### **5. Checking if a File Exists**
You can check if a file exists using the `exists` method.

#### Example:
```dart
import 'dart:io';

void main() {
  File file = File('example.txt');
  if (file.existsSync()) {
    print('File exists');
  } else {
    print('File does not exist');
  }
}
```

---

### **6. Deleting a File**
You can delete a file using the `delete` or `deleteSync` methods.

#### Example:
```dart
import 'dart:io';

void main() {
  File file = File('example.txt');
  file.deleteSync();
}
```

---

### **7. Reading and Writing Binary Data**
You can read and write binary data using the `readAsBytes` and `writeAsBytes` methods.

#### Example:
```dart
import 'dart:io';

void main() {
  File file = File('example.bin');
  file.writeAsBytesSync([0x48, 0x65, 0x6C, 0x6C, 0x6F]); // Writes 'Hello' in binary
  List<int> contents = file.readAsBytesSync();
  print(String.fromCharCodes(contents)); // Prints 'Hello'
}
```

---

### **8. Combining Properties**
Here’s an example combining multiple properties:

#### Example:
```dart
import 'dart:io';

void main() {
  File file = File('example.txt');
  if (file.existsSync()) {
    file.writeAsStringSync('Hello, Flutter!');
    print(file.readAsStringSync());
    file.deleteSync();
  } else {
    print('File does not exist');
  }
}
```

---

### **Summary of `File` Properties**
| Property              | Description                              | Example                                   |
|-----------------------|------------------------------------------|-------------------------------------------|
| `readAsString`        | Reads the file as a string               | `file.readAsStringSync()`                 |
| `writeAsString`       | Writes a string to the file              | `file.writeAsStringSync('Hello')`         |
| `exists`              | Checks if the file exists                | `file.existsSync()`                       |
| `delete`              | Deletes the file                         | `file.deleteSync()`                       |
| `readAsBytes`         | Reads the file as binary data            | `file.readAsBytesSync()`                  |
| `writeAsBytes`        | Writes binary data to the file           | `file.writeAsBytesSync([0x48, 0x65])`     |

---

### **Example: Full Usage**
Here’s a complete example of using the `File` class in a Flutter app:
```dart
import 'dart:io';
import 'package:flutter/material.dart';

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('File Example')),
        body: Center(
          child: ElevatedButton(
            onPressed: () {
              File file = File('example.txt');
              file.writeAsStringSync('Hello, Flutter!');
              String contents = file.readAsStringSync();
              print(contents);
            },
            child: Text('Read and Write File'),
          ),
        ),
      ),
    );
  }
}

void main() {
  runApp(MyApp());
}
```

---

