# react-native-modal-datetime-picker

[![npm version](https://badge.fury.io/js/react-native-modal-datetime-picker.svg)](https://badge.fury.io/js/react-native-modal-datetime-picker)
![Supports Android and iOS](https://img.shields.io/badge/platforms-android%20|%20ios-lightgrey.svg)

A declarative cross-platform react-native datetime-picker.

<p align="center">
<img src="./.github/images/datetimepicker-android.gif" height="400" />
<img src="./.github/images/datetimepicker-ios.gif" height="400" />
</p>

This library exposes a cross-platform interface for showing the native date-picker and time-picker inside a modal, providing a unified user and developer experience.

Under the hood this library is using [`@react-native-community/react-native-datetimepicker`](https://github.com/react-native-community/react-native-datetimepicker).

## Setup

Install the library and the community datetime picker using npm or yarn:

```bash
# using npm
$ npm i react-native-modal-datetime-picker @react-native-community/react-native-datetimepicker

# using yarn
$ yarn add react-native-modal-datetime-picker @react-native-community/react-native-datetimepicker
```

Please notice that the `@react-native-community/react-native-datetimepicker` package is a native module so [**it might require manual linking**](https://github.com/react-native-community/react-native-datetimepicker#getting-started).  

## Usage

```javascript
import React, { useState } from "react";
import { Button, View } from "react-native";
import DateTimePickerModal from "react-native-modal-datetime-picker";

const Example = () => {
  const [isDatePickerVisible, setDatePickerVisibility] = useState(false);

  const showDatePicker = () => {
    setDatePickerVisibility(true);
  };

  const hideDatePicker = () => {
    setDatePickerVisibility(false);
  };

  const handleConfirm = date => {
    console.warn("A date has been picked: ", date);
    hideDatePicker();
  };

  return (
    <View>
      <Button title="Show Date Picker" onPress={showDatePicker} />
      <DateTimePickerModal
        isVisible={isDatePickerVisible}
        mode="date"
        onConfirm={handleConfirm}
        onCancel={hideDatePicker}
      />
    </View>
  );
};

export default Example;
```

## Available props

| Name                    | Type      | Default       | Description                                                                                     |
| ----------------------- | --------- | ------------- | ----------------------------------------------------------------------------------------------- |
| cancelTextIOS           | string    | 'Cancel'      | The label of the cancel button (iOS)                                                            |
| confirmTextIOS          | string    | 'Confirm'     | The label of the confirm button (iOS)                                                           |
| customCancelButtonIOS   | component |               | Overrides the default cancel button component (iOS)                                             |
| customConfirmButtonIOS  | component |               | Overrides the default confirm button component (iOS)                                            |
| customHeaderIOS         | component |               | Overrides the default header component (iOS)                                                    |
| customPickerIOS         | component |               | Overrides the default native picker component (iOS)                                             |
| date                    | obj       | new Date()    | Initial selected date/time                                                                      |
| headerTextIOS           | string    | 'Pick a date' | The title text of header (iOS)                                                                  |
| isDarkModeEnabled       | bool      | false         | Is the device using a dark theme?                                                               |
| isVisible               | bool      | false         | Show the datetime picker?                                                                       |
| modalStyleIOS           | style     |               | Style of the modal content (iOS)                                                                |
| mode                    | string    | 'datetime'    | Choose between 'date', 'time', and 'datetime'                                                   |
| onCancel                | func      | **REQUIRED**  | Function called on dismiss                                                                      |
| onConfirm               | func      | **REQUIRED**  | Function called on date or time picked. It returns the date or time as a JavaScript Date object |
| onHide                  | func      | () => null    | Called after the hide animation                                                                 |
| pickerContainerStyleIOS | style     |               | The style of the picker container (iOS)                                                         |
| titleStyle              | style     |               | The style of the title text (iOS)                                                               |

👉Please notice that **all the [`@react-native-community/react-native-datetimepicker`](https://github.com/react-native-community/react-native-datetimepicker) are also supported**!

## Frequently Asked Questions

### The component is not working as expected

Under the hood `react-native-modal-datetime-picker` uses [`@react-native-community/react-native-datetimepicker`](https://github.com/react-native-community/react-native-datetimepicker).
Before reporting a bug, try swapping `react-native-datetime-picker` with [`@react-native-community/react-native-datetimepicker`](https://github.com/react-native-community/react-native-datetimepicker) and, if the issue persists, check if it has already been reported as a an issue there.

### How can I show the timepicker instead of the datepicker?

Just set the `mode` prop to `time`.
You can also display both the datepicker and the timepicker in one step by setting the `mode` prop to `datetime`.

### How do I change the color of the Android date and time pickers?

This is more a React-Native specific question than a react-native-modal-datetime-picker one.  
See issue [#29](https://github.com/mmazzarolo/react-native-modal-datetime-picker/issues/29) and [#106](https://github.com/mmazzarolo/react-native-modal-datetime-picker/issues/106) for some solutions.

### How to set 24 hours in iOS ?

The `is24Hour` prop is only available on Android but you can use a small hack for enabling it on iOS by setting the picker timezone to `en_GB`:

```js
<DatePicker
  mode="time"
  locale="en_GB" // Use "en_GB" here
  date={new Date()}
/>
```

### How to set automatic locale in iOS

Datepicker can adjust by itself locale (`fr_FR`, `en_GB`...) depending user's device locale.
Edit your `AppDelegate.m` file, and add:

```objc
// Force DatePicker locale to current language (for: 24h or 12h format, full day names etc...)
NSString *currentLanguage = [[NSLocale preferredLanguages] firstObject];
[[UIDatePicker appearance] setLocale:[[NSLocale alloc]initWithLocaleIdentifier:currentLanguage]];
```

### How do I make it work with snapshot testing?

See issue [#216](https://github.com/mmazzarolo/react-native-modal-datetime-picker/issues/216) for a possible workaround.

## Contributing

Please see the [contributing guide](./.github/CONTRIBUTING.md).

## License

The library is released under the MIT license. For more information see [`LICENSE`](/LICENSE.md).
