This vuejs component uses https://github.com/custom-select/custom-select
This one is commonly used across multiple projects


## Usage

```
<template>
 <custom-select :options="options" :optionKeys="optionKeys">
</template>

import teqCustomSelect from 'teq-custom-select"

export default {
    data:() => ({
        optionns : [
            {
                title: 'Option 1',
                val: 'Some value1',
            },
            {
                title: 'Option 2',
                val: 'Some value2',
            }
        ],

        // defaults: ['value', 'label']
        optionKeys: [
            'title', // The label field to use from options prop
            'val', // Tthe value field to use from options prop
        ],

        // Any custom select option (checkout the library : https://github.com/custom-select/custom-select)
        customSelectOptions: {},

        // Default selected value -- optional
        selectedValue: 'Some value2',

        // If you want to add a placeholder option
        placeholderOption: 'Choose an option' // default null - will not display
    })
}
```
