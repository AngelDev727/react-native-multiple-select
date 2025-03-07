## Change info

1. style custom
2. show selectedTitle with Count(optional)



## Installation

``` bash
$ npm install https://github.com/AngelDev0326/react-native-multiple-select.git#master --save
```
or use yarn

``` bash
$ yarn add https://github.com/AngelDev0326/react-native-multiple-select.git#master
```


## Updated By Angel dev: properties: <code>selectedTitleAsCount, autoFocus</code> and functions: <code>closeDropdownList, openDropdownList</code>

## On ./index.d.ts
- add selectedTitleAsCount to interface MultiSelectProps like as:

<code>selectedTitleAsCount?: boolean</code>

<code>
  closeDropdownList = () => {
    this.state.selector && this._submitSelection();
  }

  openDropdownList = () => {
    !this.state.selector && this._submitSelection();
  }
</code>
 
- add selectedTitleAsCount to propTypes and defaultProps, update function _getSelectLabel() like as:

<code>
_getSelectLabel = () => {
    const { selectText, single, selectedItems, displayKey, selectedTitleAsCount } = this.props;
    if (!selectedItems || selectedItems.length === 0) {
      return selectText;
    }
    if (single) {
      const item = selectedItems[0];
      const foundItem = this._findItem(item);
      return get(foundItem, displayKey) || selectText;
    }

    if (selectedTitleAsCount) return `${selectText} (${selectedItems.length} selected)`;
    return selectedItems.map((item) => {
      const foundItem = this._findItem(item);
      return get(foundItem, displayKey) || selectText;
    }).join(', ')
  };
</code>
  
# update this render function
<code>
render() {
    const {
      selectedItems,
      single,
      fontFamily,
      altFontFamily,
      searchInputPlaceholderText,
      searchInputStyle,
      styleDropdownMenu,
      styleDropdownMenuSubsection,
      hideSubmitButton,
      hideDropdown,
      submitButtonColor,
      submitButtonText,
      fontSize,
      textColor,
      fixedHeight,
      hideTags,
      textInputProps,
      styleMainWrapper,
      styleInputGroup,
      styleItemsContainer,
      styleSelectorContainer,
      styleTextDropdown,
      styleTextDropdownSelected,
      searchIcon,
      styleIndicator,
      autoFocus
    } = this.props;
    const { searchTerm, selector } = this.state;
    return (
      <View
        style={[
          {
            flexDirection: 'column'
          } &&
            styleMainWrapper &&
            styleMainWrapper
        ]}
      >
        {selector ? (
          <View
            style={[
              styles.selectorView(fixedHeight),
              styleSelectorContainer && styleSelectorContainer
            ]}
          >
            <View
              style={[styles.inputGroup, styleInputGroup && styleInputGroup]}
            >
              {searchIcon}
              <TextInput
                autoFocus={autoFocus}
                onChangeText={this._onChangeInput}
                onSubmitEditing={this._addItem}
                placeholder={searchInputPlaceholderText}
                placeholderTextColor={colorPack.placeholderTextColor}
                underlineColorAndroid="transparent"
                style={[searchInputStyle, { flex: 1 }]}
                value={searchTerm}
                {...textInputProps}
              />
              {hideSubmitButton && (
                <TouchableOpacity onPress={this._submitSelection}>
                  <Icon
                    name="menu-down"
                    style={[
                      styles.indicator,
                      { paddingLeft: 15, paddingRight: 15 },
                      styleIndicator && styleIndicator,
                    ]}
                  />
                </TouchableOpacity>
              )}
              {!hideDropdown && (
                <Icon
                  name="arrow-left"
                  size={20}
                  onPress={this._clearSelectorCallback}
                  color={colorPack.placeholderTextColor}
                  style={{ marginLeft: 5 }}
                />
              )}
            </View>
            <View
              style={{
                flexDirection: 'column',
                backgroundColor: '#fafafa'
              }}
            >
              <View style={styleItemsContainer && styleItemsContainer}>
                {this._renderItems()}
              </View>
              {!single && !hideSubmitButton && (
                <TouchableOpacity
                  onPress={() => this._submitSelection()}
                  style={[
                    styles.button,
                    { backgroundColor: submitButtonColor }
                  ]}
                >
                  <Text
                    style={[
                      styles.buttonText,
                      fontFamily ? { fontFamily } : {}
                    ]}
                  >
                    {submitButtonText}
                  </Text>
                </TouchableOpacity>
              )}
            </View>
          </View>
        ) : (
          <View>
            <View
              style={[
                styles.dropdownView,
                styleDropdownMenu && styleDropdownMenu
              ]}
            >
              <View
                style={[
                  styles.subSection,
                  { paddingTop: 10, paddingBottom: 10 },
                  styleDropdownMenuSubsection && styleDropdownMenuSubsection
                ]}
              >
                <TouchableWithoutFeedback onPress={this._toggleSelector}>
                  <View
                    style={{
                      flex: 1,
                      flexDirection: 'row',
                      alignItems: 'center'
                    }}
                  >
                    <Text
                      style={
                        !selectedItems || selectedItems.length === 0
                          ? [
                              {
                                flex: 1,
                                fontSize: fontSize || 16,
                                color:
                                  textColor || colorPack.placeholderTextColor
                              },
                              styleTextDropdown && styleTextDropdown,
                              altFontFamily
                                ? { fontFamily: altFontFamily }
                                : fontFamily
                                ? { fontFamily }
                                : {}
                            ]
                          : [
                              {
                                flex: 1,
                                fontSize: fontSize || 16,
                                color:
                                  textColor || colorPack.placeholderTextColor
                              },
                              styleTextDropdownSelected &&
                                styleTextDropdownSelected
                            ]
                      }
                      numberOfLines={1}
                    >
                      {this._getSelectLabel()}
                    </Text>
                    <Icon
                      name={hideSubmitButton ? 'menu-right' : 'menu-down'}
                      style={[
                        styles.indicator,
                        styleIndicator && styleIndicator,
                      ]}
                    />
                  </View>
                </TouchableWithoutFeedback>
              </View>
            </View>
            {!single && !hideTags && selectedItems.length ? (
              <View
                style={{
                  flexDirection: 'row',
                  flexWrap: 'wrap'
                }}
              >
                {this._displaySelectedItems()}
              </View>
            ) : null}
          </View>
        )}
      </View>
    );
  }
</code>

## react-native-multiple-select

[![npm](https://img.shields.io/npm/v/react-native-multiple-select.svg)](https://www.npmjs.com/package/react-native-multiple-select) [![Downloads](https://img.shields.io/npm/dt/react-native-multiple-select.svg)](https://www.npmjs.com/package/react-native-multiple-select) [![Licence](https://img.shields.io/npm/l/react-native-multiple-select.svg)](https://www.npmjs.com/package/react-native-multiple-select)

> Simple multi-select component for react-native (Select2 for react-native).

![multiple](https://user-images.githubusercontent.com/16062709/30819847-0907dd1e-a218-11e7-9980-e70b2d8e7953.gif)  ![single](https://user-images.githubusercontent.com/16062709/30819849-095d6144-a218-11e7-85b9-4e2b96f9ead9.gif)


## Usage
Note: Ensure to add and configure [react-native-vector-icons](https://github.com/oblador/react-native-vector-icons) to your project before using this package.

You can clone and try out the [sample](https://github.com/AngelDev0326/RN-multiple-select-sample) app or you can try [sample](https://github.com/AugustoAleGon/react-native-multiple-select-sample)

The snippet below shows how the component can be used


```javascript
// import component
import React, { Component } from 'react';
import { View } from 'react-native';
import MultiSelect from 'react-native-multiple-select';

const items = [{
    id: '92iijs7yta',
    name: 'Ondo'
  }, {
    id: 'a0s0a8ssbsd',
    name: 'Ogun'
  }, {
    id: '16hbajsabsd',
    name: 'Calabar'
  }, {
    id: 'nahs75a5sg',
    name: 'Lagos'
  }, {
    id: '667atsas',
    name: 'Maiduguri'
  }, {
    id: 'hsyasajs',
    name: 'Anambra'
  }, {
    id: 'djsjudksjd',
    name: 'Benue'
  }, {
    id: 'sdhyaysdj',
    name: 'Kaduna'
  }, {
    id: 'suudydjsjd',
    name: 'Abuja'
    }
];

class MultiSelectExample extends Component {

  state = {
    selectedItems : []
  };

  
  onSelectedItemsChange = selectedItems => {
    this.setState({ selectedItems });
  };

  render() {
    const { selectedItems } = this.state;

    return (
      <View style={{ flex: 1 }}>
        <MultiSelect
          hideTags
          items={items}
          uniqueKey="id"
          ref={(component) => { this.multiSelect = component }}
          onSelectedItemsChange={this.onSelectedItemsChange}
          selectedItems={selectedItems}
          selectText="Pick Items"
          searchInputPlaceholderText="Search Items..."
          onChangeInput={ (text)=> console.log(text)}
          altFontFamily="ProximaNova-Light"
          tagRemoveIconColor="#CCC"
          tagBorderColor="#CCC"
          tagTextColor="#CCC"
          selectedItemTextColor="#CCC"
          selectedItemIconColor="#CCC"
          itemTextColor="#000"
          displayKey="name"
          searchInputStyle={{ color: '#CCC' }}
          submitButtonColor="#CCC"
          submitButtonText="Submit"
        />
        <View>
          {this.multiSelect.getSelectedItemsExt(selectedItems)}
        </View>
      </View>
    );
  }
}

```

The component takes 3 compulsory props - `items`, `uniqueKey` and `onSelectedItemsChange`. Other props are optional. The table below explains more.


## Props

| Prop        | Required   | Purpose  |
| ------------- |-------------| -----|
| altFontFamily | No      | (String) Font family for `searchInputPlaceholderText` |
| canAddItems | No      | (Boolean) Defaults to "false". This allows a user to add items to the list of items provided. You need to handle adding the new items in the onAddItem function prop. Items may be added with the return key on the native keyboard. |
| displayKey | No | (String) Defaults to "name". This string will be used to select the key to display the objects in the items array |
| fixedHeight | No     | (Boolean) Defaults to false. Specifies if select dropdown take height of content or a fixed height with a scrollBar (There is an issue with this behavior when component is nested in a ScrollView in which scroll event will only be dispatched to parent ScrollView and select component won't be scrollable). See [this issue](https://github.com/AngelDev0326/react-native-multiple-select/issues/12) for more info. |
| filterMethod | No | (String) Defaults to  "partial". options: ["partial", "full"] Choose the logic on how the system filters items based on searchTerm. partial: checks all individual words and if at least one word matches will include that item. full: checks to ensure the item contains the full substring of searchterm in order minus any leading or trailing spaces.
| flatListProps | No | (Object) Properties for the FlatList. Pass any property that is required on the FlatList of the dropdown menu |
| fontFamily | No     | (String) Custom font family to be used in component (affects all text except `searchInputPlaceholderText` described above) |
| fontSize | No     | (Number) Font size for selected item name displayed as label for multiselect |
| hideDropdown | No | (Boolean) Defaults false. Hide dropdown menu with a cancel, and use arrow-back |
| hideSubmitButton | No | (Boolean) Defaults to false. Hide submit button from dropdown, and rather use arrow-button in search field |
| hideTags | No | (Boolean) Defaults to false. Hide tokenized selected items, in case selected items are to be shown somewhere else in view (check below for more info) |
| iconSearch | No | (Element, Object, boolean, Function) Element or functional component to change the Search Icon |
| itemFontFamily | No   | (String) Font family for each non-selected item in multi-select drop-down |
| itemFontSize | No   | (Number) Font size used for each item in the multi-select drop-down |
| itemTextColor | No   | (String) Text color for each non-selected item in multi-select drop-down |
| items      | Yes | (Array, control prop) List of items to display in the multi-select component. JavaScript Array of objects. Each object must contain a name and unique identifier (Check sample above) |
|noItemsText| No| (String) Text that replace default "no items to display"|
| onAddItem | No   | (Function) JavaScript function passed in as an argument. The function is called everytime a new item is added, and receives the entire list of items. Here you should ensure that the new items are added to your provided list of `items` in addition to any other consequences of new items being added. |
| onChangeInput | No    | (Function) JavaScript function passed in as an argument. The function is called everytime `TextInput` is changed with the value. |
| onClearSelector | No | (Function) JavaScript function passeed in as an argument. The function is called everytime `back button` is pressed |
| onSelectedItemsChange | Yes      | (Function) JavaScript function passed in as an argument. The function is to be defined with an argument (selectedItems). Triggered when `Submit` button is clicked (for multi select) or item is clicked (for single select). (Check sample above) |
| onToggleList | No | (Function) JavaScript function passed in as an argument. The function is called everytime the `multiselect` component is pressed |
| searchInputPlaceholderText | No      | (String) Placeholder text displayed in multi-select filter input |
| searchInputStyle | No   | (Object) Style object for multi-select input element  |
| selectText | No     | (String) Text displayed in main component |
| selectedText | No | (String) Text displayed when an item is selected can be replaced by any string|
| selectedItemFontFamily | No   | (String) Font family for each selected item in multi-select drop-down |
| selectedItemIconColor | No     | (String) Color for `selected` check icon for each selected item in multi-select drop-down |
| selectedItemTextColor | No   | (String) Text color for each selected item in multi-select drop-down |
| single | No     | (Boolean) Toggles select component between single option and multi option |
| styleDropdownMenu | No | (Style) Style the view of the dropdown menu |
| styleDropdownMenuSubsection | No | (Style) Style the inner view of the dropdown menu |
| styleIndicator | No | (Style) Style the Icon for indicator |
| styleInputGroup | No | (Style) Style the Container of the Text Input Group |
| styleItemsContainer | No | (Style) Style the Container of the items that are displayed in a list |
| styleListContainer | No | (Style) Style the Container of main list. See [this issue] (https://github.com/AngelDev0326/react-native-multiple-select/issues/12)|
| styleMainWrapper | No | (Style) Style the Main Container of the MultiSelector |
| styleRowList | No | (Style) Style the Row that is displayed after you |
| styleSelectorContainer | No | (Style) Style the Container of the Selector when user clicks on the dropdown|
| styleTextDropdown | No | (Text Style) Style text of the Dropdown |
| styleTextDropdownSelected | No | (Text Style) Style text of the Dropdown selected |
| styleTextTag | No | (Text Style) Style text of the tag |
| submitButtonColor | No   | (String) Background color for submit button  |
| submitButtonText | No   | (String) Text displayed on submit button  |
| tagBorderColor | No      | (String) Border color for each selected item  |
| tagContainerStyle | No | (Style) Style the container of the tag view |
| tagRemoveIconColor | No      | (String) Color to be used for the remove icon in selected items list |
| tagTextColor | No  | (String) Text color for selected items list |
| textColor | No     | (String) Color for selected item name displayed as label for multiselect  |
| textInputProps | No | (Object) Properties for the Text Input. Pass any property that is required on the text input |
| uniqueKey      | Yes      | (String) Unique identifier that is part of each item's properties. Used internally as means of identifying each item (Check sample below) |
|selectedItems | No      | (Array, control prop) List of selected items keys . JavaScript Array of strings, that can be instantiated with the component |
| removeSelected | No  | (Boolean) Filter selected items from list to be shown in List |

## Note

- Tokenized selected items can be displayed in any other part of the view by adding a `ref` to the `MultiSelect` component like so `ref={(component) => { this.multiSelect = component }}`. Then add this to any part of the screen you want the tokens to show up: `this.multiSelect.getSelectedItemsExt(selectedItems)`. The `selectedItems` argument passed into the above mentioned method is the same `selectedItems` passed as the main component selected items prop. (See example above).

- If users shouldn't be able to select any of the items in the dropdown list, set a `disabled` key to true in the item. Such item will be rendered in gray and won't be clickable.

- When using the `single` prop, `selectedItems` should still be passed in as an array of selected items keys. Also, when an item is selected in the single mode, the selected item is returned as an array of string.

- The `items` props must be passed as an array of objects with a compulsory `name` key present in each object as the name key is used to display the items in the options component.

- filterMethod partial example: searchTerm = "University of New" will return "University of New York", "University of New Orleans", "The University of New York" as well as "University of Columbia" and "New England Tech" due to partial matches.

- filterMethod full example: searchTerm = "University of New" will return" University of New York", "University of New Orleans", "The University of New York" because all three contain the substring "University of New"

### Removing all selected items

To use, add ref to MultiSelect component in parent component, then call method against reference. i.e.

```javascript
<MultiSelect
  ref={multiSelectRef}
  ...
/>

const clearSelectedCategories = () => {
   multiSelectRef.removeAllItems();
};

```
