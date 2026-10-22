# Effectively scale UI according to different screen sizes

A small Flutter app that shows how to size widgets and text as a percentage of the screen, so the same layout scales across phones and tablets. The code follows the Flutter Community article "Flutter - Effectively scale UI according to different screen sizes" on Medium.

## How it works

`lib/size_config.dart` has a `SizeConfig` class. Call `SizeConfig().init(context)` at the top of a `build` method and it reads `MediaQuery` to work out:

- `screenWidth` and `screenHeight`
- `blockSizeHorizontal` and `blockSizeVertical`: 1% of the screen width or height
- `safeBlockHorizontal` and `safeBlockVertical`: 1% of the width or height after subtracting safe-area padding (notches, status bar)

Sizes are then written as multiples of those blocks:

```dart
SizeConfig().init(context);

Text(
  'Scaling text!',
  style: TextStyle(fontSize: SizeConfig.safeBlockHorizontal! * 10),
);

Container(
  height: SizeConfig.safeBlockVertical! * 25,
  width: SizeConfig.safeBlockHorizontal! * 55,
);
```

`lib/main.dart` has two demo screens. `TextScalePage` (the one the app opens on) shows text sized at 10% of the safe width. `MyHomePage` shows a box that is 55% wide and 25% tall. To see the box, change `home:` in `MyApp` to `MyHomePage()`.

## Running it

The project was created in 2022 on the Flutter beta channel (Dart 2.17 beta, null safety). It has no dependencies beyond the Flutter SDK and `cupertino_icons`.

```
flutter pub get
flutter run
```

Android, iOS and web platform folders are included.

`test/widget_test.dart` is still the default counter test from `flutter create` and doesn't match this app, so `flutter test` will fail.
