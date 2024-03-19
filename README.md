
# WHAT IS STATE MANAGEMENT ?
A cleaner way to sotre the state of your app ,
Until now , the cleanest thing you can do is use context API.

But there are better solutions that get rid of the problem that context API has ( unnecessary re-renders)

# What is Recoil ?
It is a state management library :

STEP 1 : Create a folder name store -> atom -> count.jsx

`count.jsx`
```jsx
import {atom} form 'recoil';
const countAtom = atom ({
 key : "countAtom " , // Unique id: (with respect to other atoms/ selectors : )
    default : 0 , // Default value (aka initial value : )
})
export default countAtom
```
