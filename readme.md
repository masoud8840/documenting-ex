
# SearchInput.vue
Shorten your search inputs like a hero...

## Variables
### Available because of the user to be able to hide or unhide the input

| Parameter   | Type     |
:--------     | :------- |
| `expanded`  | `boolean`|

## Methods
### clickOutside
Called when user clicked outside of parent element to toggling input off. The event listener is registered on onMounted hook and will unregistered onUnmounted hook

### onSubmit
Called when user try to submit the form which is parent element of input to register onSubmit emit

### onChange
Called when user try to change the value of input to register onChange emit

## Props
### The input value, or v-model property of its value

| Parameter   | Type     | Required / Default value   |
| :--------   | :------- | :------------------------- |
| `searchText`| `string` | required            |

#### ex:
```
<SearchInput v-model="searchText" />
```

### The placeholder of SearchInput

| Parameter    | Type     | Required / Default value  |
| :--------    | :------- | :-------------------------|
| `placeholder`| `string` | required            |

#### ex:
```
<SearchInput v-model="searchText" 
             placeholder="some placeholder in here"
/>
```

## Emits
### onSubmit
Return a string passed through an simple regex
| Parameter    | Return Type |
| :--------    | :-------    | 
| `onChange`   | `string`    |

#### ex:
```
<SearchInput v-model="searchText" 
             placeholder="some placeholder in here"
             @onChange=(value)=>(console.log(value))
/>
```

### onChange
Same as onSubmit emit returns a string passed through a simple regex
| Parameter    | Return Type |
| :--------    | :-------    | 
| `onSubmit`   | `string`    |

#### ex:
```
<SearchInput v-model="searchText" 
             placeholder="some placeholder in here"
             @onChange=(value)=>(console.log(value))
             @onSubmit=(value)=>(console.log(value))
/>
```